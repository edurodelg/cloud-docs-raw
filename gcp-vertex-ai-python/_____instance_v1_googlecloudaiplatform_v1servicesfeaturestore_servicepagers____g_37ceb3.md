---
merged_at: 2026-01-27T07:03:44.005994
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/instance_v1 -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest -->

# Class AssessDataRequest (1.134.0)

`AssessDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets.

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
`tuning_validation_assessment_config` |
Optional. Configuration for the tuning validation assessment. This field is a member of `oneof` _ `assessment_config` .
|
`tuning_resource_usage_assessment_config` |
Optional. Configuration for the tuning resource usage assessment. This field is a member of `oneof` _ `assessment_config` .
|
`batch_prediction_validation_assessment_config` |
Optional. Configuration for the batch prediction validation assessment. This field is a member of `oneof` _ `assessment_config` .
|
`batch_prediction_resource_usage_assessment_config` |
Optional. Configuration for the batch prediction resource usage assessment. This field is a member of `oneof` _ `assessment_config` .
|
`name` |
`str`
Required. The name of the Dataset resource. Used only for MULTIMODAL datasets. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`gemini_request_read_config` |
Optional. The Gemini request read config for the dataset. |

## Classes

### BatchPredictionResourceUsageAssessmentConfig

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.

### BatchPredictionValidationAssessmentConfig

```
BatchPredictionValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction validation assessment.

### TuningResourceUsageAssessmentConfig

```
TuningResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning resource usage assessment.

### TuningValidationAssessmentConfig

```
TuningValidationAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the tuning validation assessment.

## Methods

### AssessDataRequest

`AssessDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelBatchPredictionJobRequest -->

# Class CancelBatchPredictionJobRequest (1.134.0)

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob to cancel. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### CancelBatchPredictionJobRequest

```
CancelBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataRequest -->

# Class ImportDataRequest (1.134.0)

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`import_configs` |
`MutableSequence[`
Required. The desired input locations. The contents of all input locations will be imported in one batch. |

## Methods

### ImportDataRequest

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateMemoryRequest -->

# Class UpdateMemoryRequest (1.134.0)

`UpdateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.UpdateMemory.

## Attributes |
|
|---|---|
Name |
Description |
`memory` |
Required. The Memory which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. Supported fields: :: * `display_name`
* `description`
* `fact`
|

## Methods

### UpdateMemoryRequest

`UpdateMemoryRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.UpdateMemory.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateRequest -->

# Class CheckTrialEarlyStoppingStateRequest (1.134.0)

```
CheckTrialEarlyStoppingStateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VizierService.CheckTrialEarlyStoppingState.

## Attribute |
|
|---|---|
Name |
Description |
`trial_name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### CheckTrialEarlyStoppingStateRequest

```
CheckTrialEarlyStoppingStateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VizierService.CheckTrialEarlyStoppingState.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresAsyncPager -->

# Class ListFeatureOnlineStoresAsyncPager (1.134.0)

```
ListFeatureOnlineStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse) object, and
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

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureOnlineStoresAsyncPager

```
ListFeatureOnlineStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureMonitorRequest -->

# Class DeleteFeatureMonitorRequest (1.134.0)

`DeleteFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.DeleteFeatureMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureMonitor to be deleted. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}`
|

## Methods

### DeleteFeatureMonitorRequest

`DeleteFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.DeleteFeatureMonitor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.VertexVectorSearch -->

# Class VertexVectorSearch (1.134.0)

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`index` |
`str`
The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### VertexVectorSearch

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service -->

# Package specialist_pool_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.specialist_pool_service`

package.

## Classes

[SpecialistPoolServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceAsyncClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

[SpecialistPoolServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.SpecialistPoolServiceClient)

A service for creating and managing Customer SpecialistPools. When customers start Data Labeling jobs, they can reuse/create Specialist Pools to bring their own Specialists to label the data. Customers can add/remove Managers for the Specialist Pool on Cloud console, then Managers will get email notifications to manage Specialists and tasks on CrowdCompute console.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers)

API documentation for `aiplatform_v1beta1.services.specialist_pool_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExamplesRestrictionsNamespace -->

# Class ExamplesRestrictionsNamespace (1.134.0)

```
ExamplesRestrictionsNamespace(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Restrictions namespace for example-based explanations overrides.

## Attributes |
|
|---|---|
Name |
Description |
`namespace_name` |
`str`
The namespace name. |
`allow` |
`MutableSequence[str]`
The list of allowed tags. |
`deny` |
`MutableSequence[str]`
The list of deny tags. |

## Methods

### ExamplesRestrictionsNamespace

```
ExamplesRestrictionsNamespace(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Restrictions namespace for example-based explanations overrides.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreRequest -->

# Class CreateExampleStoreRequest (1.134.0)

`CreateExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.CreateExampleStore.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ExampleStore in. Format: `projects/{project}/locations/{location}`
|
`example_store` |
Required. The Example Store to be created. |

## Methods

### CreateExampleStoreRequest

`CreateExampleStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.CreateExampleStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteTrainingPipelineRequest -->

# Class DeleteTrainingPipelineRequest (1.134.0)

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TrainingPipeline resource to be deleted. Format: `projects/{project}/locations/{location}/trainingPipelines/{training_pipeline}`
|

## Methods

### DeleteTrainingPipelineRequest

```
DeleteTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.DeleteTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexRequest -->

# Class UpdateIndexRequest (1.134.0)

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index` |
Required. The Index which updates the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateIndexRequest

`UpdateIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.UpdateIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.TcpSocketAction -->

# Class TcpSocketAction (1.134.0)

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

## Attributes |
|
|---|---|
Name |
Description |
`port` |
`int`
Number of the port to access on the container. Number must be in the range 1 to 65535. |
`host` |
`str`
Optional: Host name to connect to, defaults to the model serving container's IP. |

## Methods

### TcpSocketAction

`TcpSocketAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TcpSocketAction probes the health of a container by opening a TCP socket connection.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentResponse.PromptFeedback.BlockedReason -->

# Class BlockedReason (1.134.0)

`BlockedReason(value)`


Blocked reason enumeration.

## Enums |
|
|---|---|
Name |
Description |
`BLOCKED_REASON_UNSPECIFIED` |
Unspecified blocked reason. |
`SAFETY` |
Candidates blocked due to safety. |
`OTHER` |
Candidates blocked due to other reason. |
`BLOCKLIST` |
Candidates blocked due to the terms which are included from the terminology blocklist. |
`PROHIBITED_CONTENT` |
Candidates blocked due to prohibited content. |
`MODEL_ARMOR` |
The user prompt was blocked by Model Armor. |

## Methods

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel -->

# Class DeployedModel (1.134.0)

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

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
`dedicated_resources` |
A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`automatic_resources` |
A description of resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. This field is a member of `oneof` _ `prediction_resources` .
|
`shared_resources` |
`str`
The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
This field is a member of `oneof` _ `prediction_resources` .
|
`full_fine_tuned_resources` |
Optional. Resources for a full fine tuned model. This field is a member of `oneof` _ `prediction_resources` .
|
`id` |
`str`
Immutable. The ID of the DeployedModel. If not provided upon deployment, Vertex AI will generate a value for this ID. This value should be 1-10 characters, and valid characters are `/[0-9]/` .
|
`model` |
`str`
The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint. The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
|
`model_version_id` |
`str`
Output only. The version ID of the model that is deployed. |
`display_name` |
`str`
The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedModel was created. |
`explanation_spec` |
Explanation configuration for this DeployedModel. When deploying a Model using EndpointService.DeployModel, this value overrides the value of Model.explanation_spec. All fields of explanation_spec are optional in the request. If a field of explanation_spec is not populated, the value of the same field of Model.explanation_spec is inherited. If the corresponding Model.explanation_spec is not populated, all fields of the explanation_spec will be used for the explanation configuration. |
`disable_explanations` |
`bool`
If true, deploy the model without explainable feature, regardless the existence of Model.explanation_spec or explanation_spec. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`enable_container_logging` |
`bool`
If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging.
Only supported for custom-trained Models and AutoML Tabular
Models.
|
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`enable_access_logging` |
`bool`
If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request. Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`private_endpoints` |
Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if network is configured. |
`faster_deployment_config` |
Configuration for faster model deployment. |
`rollout_options` |
Options for configuring rolling deployments. |
`status` |
Output only. Runtime status of the deployed model. |
`system_labels` |
`MutableMapping[str, str]`
System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`checkpoint_id` |
`str`
The checkpoint id of the model. |
`speculative_decoding_spec` |
Optional. Spec for configuring speculative decoding. |

## Classes

### Status

`Status(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime status of the deployed model.

### SystemLabelsEntry

`SystemLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeployedModel

`DeployedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of a Model. Endpoints contain one or more DeployedModels.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient -->

# Class DataFoundryServiceAsyncClient (1.134.0)

```
DataFoundryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for generating and preparing datasets for Gen AI evaluation.

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
`DataFoundryServiceTransport` |
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

### DataFoundryServiceAsyncClient

```
DataFoundryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the data foundry service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DataFoundryServiceTransport,Callable[..., DataFoundryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the DataFoundryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`DataFoundryServiceAsyncClient` |
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
`DataFoundryServiceAsyncClient` |
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
`DataFoundryServiceAsyncClient` |
The constructed client. |

### generate_synthetic_data

```
generate_synthetic_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataRequest,
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
google.cloud.aiplatform_v1.types.data_foundry_service.GenerateSyntheticDataResponse
)
```


Generates synthetic data based on the provided configuration.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_generate_synthetic_data():
# Create a client
client = aiplatform_v1.
```[DataFoundryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient.html)()
# Initialize request argument(s)
task_description = aiplatform_v1.[TaskDescriptionStrategy](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TaskDescriptionStrategy.html)()
task_description.task_description = "task_description_value"
output_field_specs = aiplatform_v1.[OutputFieldSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.OutputFieldSpec.html)()
output_field_specs.field_name = "field_name_value"
request = aiplatform_v1.[GenerateSyntheticDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataRequest.html)(
task_description=task_description,
location="location_value",
count=553,
output_field_specs=output_field_specs,
)
# Make the request
response = await client.[generate_synthetic_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.data_foundry_service.DataFoundryServiceAsyncClient.html#google_cloud_aiplatform_v1_services_data_foundry_service_DataFoundryServiceAsyncClient_generate_synthetic_data)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for DataFoundryService.GenerateSyntheticData. |
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
The response containing the generated data. |

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
google.cloud.aiplatform_v1.services.data_foundry_service.transports.base.DataFoundryServiceTransport
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessSpec -->

# Class QuestionAnsweringCorrectnessSpec (1.134.0)

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering correctness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringCorrectnessSpec

```
QuestionAnsweringCorrectnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering correctness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse -->

# Class ListPersistentResourcesResponse (1.134.0)

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources

## Attribute |
|
|---|---|
Name |
Description |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListPersistentResourcesRequest.page_token to obtain that page. |

## Methods

### ListPersistentResourcesResponse

```
ListPersistentResourcesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for PersistentResourceService.ListPersistentResources

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessSpec -->

# Class QuestionAnsweringHelpfulnessSpec (1.134.0)

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering helpfulness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### QuestionAnsweringHelpfulnessSpec

```
QuestionAnsweringHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering helpfulness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexOperationMetadata -->

# Class CreateIndexOperationMetadata (1.134.0)

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### CreateIndexOperationMetadata

```
CreateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.CreateIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsPager -->

# Class ListDeploymentResourcePoolsPager (1.134.0)

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__iter__`

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

### ListDeploymentResourcePoolsPager

```
ListDeploymentResourcePoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.session_service.pagers`

module.

## Classes

[ListEventsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsAsyncPager)

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

[ListEventsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsPager)

```
ListEventsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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


A pager for iterating through `list_events`

requests.

This class thinly wraps an initial
[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse) object, and
provides an `__iter__`

method to iterate through its
`session_events`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEvents`

requests and continue to iterate
through the `session_events`

field on the
corresponding responses.

All the usual [ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSessionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsAsyncPager)

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

[ListSessionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsPager)

```
ListSessionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


A pager for iterating through `list_sessions`

requests.

This class thinly wraps an initial
[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse) object, and
provides an `__iter__`

method to iterate through its
`sessions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSessions`

requests and continue to iterate
through the `sessions`

field on the
corresponding responses.

All the usual [ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesAsyncPager -->

# Class ListNotebookRuntimeTemplatesAsyncPager (1.134.0)

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__aiter__`

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

### ListNotebookRuntimeTemplatesAsyncPager

```
ListNotebookRuntimeTemplatesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringStatsAsyncPager -->

# Class SearchModelMonitoringStatsAsyncPager (1.134.0)

```
SearchModelMonitoringStatsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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


A pager for iterating through `search_model_monitoring_stats`

requests.

This class thinly wraps an initial
[SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

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

### SearchModelMonitoringStatsAsyncPager

```
SearchModelMonitoringStatsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse -->

# Class ListSessionsResponse (1.134.0)

`ListSessionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListSessions.

## Attributes |
|
|---|---|
Name |
Description |
`sessions` |
`MutableSequence[`
A list of sessions matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListSessionsRequest.page_token to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### ListSessionsResponse

`ListSessionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListSessions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schedule.State -->

# Class State (1.134.0)

`State(value)`


Possible state of the schedule.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`ACTIVE` |
The Schedule is active. Runs are being scheduled on the user-specified timespec. |
`PAUSED` |
The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete. |
`COMPLETED` |
The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## Methods

### State

`State(value)`


Possible state of the schedule.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexEndpointRequest -->

# Class CreateIndexEndpointRequest (1.134.0)

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: `projects/{project}/locations/{location}`
|
`index_endpoint` |
Required. The IndexEndpoint to create. |

## Methods

### CreateIndexEndpointRequest

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexOperationMetadata -->

# Class UpdateIndexOperationMetadata (1.134.0)

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`nearest_neighbor_search_operation_metadata` |
The operation metadata with regard to Matching Engine Index operation. |

## Methods

### UpdateIndexOperationMetadata

```
UpdateIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexService.UpdateIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetModelEvaluationSliceRequest -->

# Class GetModelEvaluationSliceRequest (1.134.0)

```
GetModelEvaluationSliceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.GetModelEvaluationSlice.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`
|

## Methods

### GetModelEvaluationSliceRequest

```
GetModelEvaluationSliceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.GetModelEvaluationSlice.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataRequest -->

# Class ImportDataRequest (1.134.0)

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`import_configs` |
`MutableSequence[`
Required. The desired input locations. The contents of all input locations will be imported in one batch. |

## Methods

### ImportDataRequest

`ImportDataRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ImportData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient -->

# Class LlmUtilityServiceAsyncClient (1.134.0)

```
LlmUtilityServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for LLM related utility functions.

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
`LlmUtilityServiceTransport` |
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

### LlmUtilityServiceAsyncClient

```
LlmUtilityServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the llm utility service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,LlmUtilityServiceTransport,Callable[..., LlmUtilityServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the LlmUtilityServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### compute_tokens

```
compute_tokens(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
instances: typing.Optional[
typing.MutableSequence[google.protobuf.struct_pb2.Value]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.llm_utility_service.ComputeTokensResponse
```


Return a list of tokens based on the input text.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_compute_tokens():
# Create a client
client = aiplatform_v1beta1.
```[LlmUtilityServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ComputeTokensRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ComputeTokensRequest.html)(
endpoint="endpoint_value",
)
# Make the request
response = await client.[compute_tokens](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.llm_utility_service.LlmUtilityServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_llm_utility_service_LlmUtilityServiceAsyncClient_compute_tokens)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ComputeTokens RPC call. |
`endpoint` |
Required. The name of the Endpoint requested to get lists of tokens and token ids. This corresponds to the |
`instances` |
`:class:`
Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models. This corresponds to the |
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
Response message for ComputeTokens RPC call. |

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
`LlmUtilityServiceAsyncClient` |
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
`LlmUtilityServiceAsyncClient` |
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
`LlmUtilityServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.llm_utility_service.transports.base.LlmUtilityServiceTransport
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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/instance_v1beta1 -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictResponse -->

# Class PredictResponse (1.134.0)

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. The schema of any single prediction may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] prediction_schema_uri. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this prediction. |
`model` |
`str`
Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_version_id` |
`str`
Output only. The version ID of the Model which is deployed as the DeployedModel that this prediction hits. |
`model_display_name` |
`str`
Output only. The [display name][google.cloud.aiplatform.v1beta1.Model.display_name] of the Model which is deployed as the DeployedModel that this prediction hits. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation. |

## Methods

### PredictResponse

`PredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Predict.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportDataOperationMetadata -->

# Class ExportDataOperationMetadata (1.134.0)

`ExportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ExportData.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`gcs_output_directory` |
`str`
A Google Cloud Storage directory which path ends with '/'. The exported data is stored in the directory. |

## Methods

### ExportDataOperationMetadata

`ExportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ExportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataResponse -->

# Class ExportDataResponse (1.134.0)

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

## Attribute |
|
|---|---|
Name |
Description |
`exported_files` |
`MutableSequence[str]`
All of the files that are exported in this export operation. For custom code training export, only three (training, validation and test) Cloud Storage paths in wildcard format are populated (for example, gs://.../training-\*). |

## Methods

### ExportDataResponse

`ExportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ExportData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.VertexVectorSearch -->

# Class VertexVectorSearch (1.134.0)

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`index` |
`str`
The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### VertexVectorSearch

`VertexVectorSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Vertex Vector Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesRestrictionsNamespace -->

# Class ExamplesRestrictionsNamespace (1.134.0)

```
ExamplesRestrictionsNamespace(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Restrictions namespace for example-based explanations overrides.

## Attributes |
|
|---|---|
Name |
Description |
`namespace_name` |
`str`
The namespace name. |
`allow` |
`MutableSequence[str]`
The list of allowed tags. |
`deny` |
`MutableSequence[str]`
The list of deny tags. |

## Methods

### ExamplesRestrictionsNamespace

```
ExamplesRestrictionsNamespace(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Restrictions namespace for example-based explanations overrides.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Predictor -->

# Class Predictor (1.134.0)

`Predictor()`


Interface of the Predictor class for Custom Prediction Routines.

The Predictor is responsible for the ML logic for processing a prediction request. Specifically, the Predictor must define: (1) How to load all model artifacts used during prediction into memory. (2) The logic that should be executed at predict time.

When using the default `PredictionHandler`

, the `Predictor`

will be invoked as
follows:

```
predictor.postprocess(predictor.predict(predictor.preprocess(prediction_input)))
```


## Methods

### load

`load(artifacts_uri: str) -> None`


Loads the model artifact.

Parameter |
|
|---|---|
Name |
Description |
`artifacts_uri` |
`str`
Required. The value of the environment variable AIP_STORAGE_URI. |

### postprocess

`postprocess(prediction_results: typing.Any) -> typing.Any`


Postprocesses the prediction results.

Parameter |
|
|---|---|
Name |
Description |
`prediction_results` |
`Any`
Required. The prediction results. |

### predict

`predict(instances: typing.Any) -> typing.Any`


Performs prediction.

Parameter |
|
|---|---|
Name |
Description |
`instances` |
`Any`
Required. The instance(s) used for performing prediction. |

### preprocess

`preprocess(prediction_input: typing.Any) -> typing.Any`


Preprocesses the prediction input before doing the prediction.

Parameter |
|
|---|---|
Name |
Description |
`prediction_input` |
`Any`
Required. The prediction input that needs to be preprocessed. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SmoothGradConfig -->

# Class SmoothGradConfig (1.134.0)

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

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
`noise_sigma` |
`float`
This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range [0, 1], [-1, 1] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about `normalization ` __.
For best results the recommended value is about 10% - 20% of
the standard deviation of the input feature. Refer to
section 3.2 of the SmoothGrad paper:
https://arxiv.org/pdf/1706.03825.pdf. Defaults to 0.1.
If the distribution is different per feature, set
feature_noise_sigma
instead for each feature.
This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`feature_noise_sigma` |
This is similar to noise_sigma, but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, noise_sigma will be used for all features. This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`noisy_sample_count` |
`int`
The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is [1, 50]. Defaults to 3. |

## Methods

### SmoothGradConfig

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse -->

# Class ListContextsResponse (1.134.0)

`ListContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListContexts.

## Attributes |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
The Contexts retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListContextsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListContextsResponse

`ListContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateSpecialistPoolRequest -->

# Class CreateSpecialistPoolRequest (1.134.0)

`CreateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.CreateSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent Project name for the new SpecialistPool. The form is `projects/{project}/locations/{location}` .
|
`specialist_pool` |
Required. The SpecialistPool to create. |

## Methods

### CreateSpecialistPoolRequest

`CreateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.CreateSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsRequest -->

# Class ListTensorboardExperimentsRequest (1.134.0)

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`filter` |
`str`
Lists the TensorboardExperiments that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardExperiments to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardExperiments are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardExperiments call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardExperiments must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardExperimentsRequest

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SmoothGradConfig -->

# Class SmoothGradConfig (1.134.0)

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

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
`noise_sigma` |
`float`
This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range [0, 1], [-1, 1] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about `normalization ` __.
For best results the recommended value is about 10% - 20% of
the standard deviation of the input feature. Refer to
section 3.2 of the SmoothGrad paper:
https://arxiv.org/pdf/1706.03825.pdf. Defaults to 0.1.
If the distribution is different per feature, set
feature_noise_sigma
instead for each feature.
This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`feature_noise_sigma` |
This is similar to noise_sigma, but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, noise_sigma will be used for all features. This field is a member of `oneof` _ `GradientNoiseSigma` .
|
`noisy_sample_count` |
`int`
The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is [1, 50]. Defaults to 3. |

## Methods

### SmoothGradConfig

`SmoothGradConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details:

[https://arxiv.org/pdf/1706.03825.pdf](https://arxiv.org/pdf/1706.03825.pdf)

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PointwiseMetricSpec -->

# Class PointwiseMetricSpec (1.134.0)

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pointwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|
`system_instruction` |
`str`
Optional. System instructions for pointwise metric. This field is a member of `oneof` _ `_system_instruction` .
|
`custom_output_format_config` |
Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation`
fields in the corresponding metric result will be empty.
|

## Methods

### PointwiseMetricSpec

`PointwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pointwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteMetadataStoreRequest -->

# Class DeleteMetadataStoreRequest (1.134.0)

`DeleteMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the MetadataStore to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`force` |
`bool`
Deprecated: Field is no longer supported. |

## Methods

### DeleteMetadataStoreRequest

`DeleteMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteMetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteBatchPredictionJobRequest -->

# Class DeleteBatchPredictionJobRequest (1.134.0)

```
DeleteBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob resource to be deleted. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### DeleteBatchPredictionJobRequest

```
DeleteBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteBatchPredictionJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager -->

# Class ListModelDeploymentMonitoringJobsAsyncPager (1.134.0)

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

## Methods

### ListModelDeploymentMonitoringJobsAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetDeploymentResourcePoolRequest -->

# Class GetDeploymentResourcePoolRequest (1.134.0)

```
GetDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for GetDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DeploymentResourcePool to retrieve. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|

## Methods

### GetDeploymentResourcePoolRequest

```
GetDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for GetDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddTrialMeasurementRequest -->

# Class AddTrialMeasurementRequest (1.134.0)

`AddTrialMeasurementRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.AddTrialMeasurement.

## Attributes |
|
|---|---|
Name |
Description |
`trial_name` |
`str`
Required. The name of the trial to add measurement. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`measurement` |
Required. The measurement to be added to a Trial. |

## Methods

### AddTrialMeasurementRequest

`AddTrialMeasurementRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.AddTrialMeasurement.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesResponse.UpsertResult -->

# Class UpsertResult (1.134.0)

`UpsertResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result for creating/updating a single example.

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
`example` |
The example created/updated successfully. This field is a member of `oneof` _ `result` .
|
`status` |
`google.rpc.status_pb2.Status`
The error message of the example that was not created/updated successfully. This field is a member of `oneof` _ `result` .
|

## Methods

### UpsertResult

`UpsertResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result for creating/updating a single example.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataAsyncPager -->

# Class ExportTensorboardTimeSeriesDataAsyncPager (1.134.0)

```
ExportTensorboardTimeSeriesDataAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__aiter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__aiter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ExportTensorboardTimeSeriesDataAsyncPager

```
ExportTensorboardTimeSeriesDataAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointRequest -->

# Class UpdateEndpointRequest (1.134.0)

`UpdateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UpdateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateEndpointRequest

`UpdateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UpdateEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.BigQuerySourceConfig -->

# Class BigQuerySourceConfig (1.134.0)

`BigQuerySourceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from a BigQuery table.

## Methods

### BigQuerySourceConfig

`BigQuerySourceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from a BigQuery table.

## Attributes |
|
|---|---|
Name |
Description |
`table_path` |
`str`
Required. The path to the BigQuery table containing the index data, in the format of `bq://` .
|
`datapoint_field_mapping` |
Required. Mapping of datapoint fields to BigQuery column names. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexEndpointRequest -->

# Class CreateIndexEndpointRequest (1.134.0)

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the IndexEndpoint in. Format: `projects/{project}/locations/{location}`
|
`index_endpoint` |
Required. The IndexEndpoint to create. |

## Methods

### CreateIndexEndpointRequest

`CreateIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.CreateIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureViewRequest -->

# Class DeleteFeatureViewRequest (1.134.0)

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureOnlineStoreAdminService.DeleteFeatureViews][].

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureView to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### DeleteFeatureViewRequest

`DeleteFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeatureOnlineStoreAdminService.DeleteFeatureViews][].

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest -->

# Class DeployRequest (1.134.0)

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
`publisher_model_name` |
`str`
The Model Garden model to deploy. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .
This field is a member of `oneof` _ `artifacts` .
|
`hugging_face_model_id` |
`str`
The Hugging Face model to deploy. Format: Hugging Face model ID like `google/gemma-2-2b-it` .
This field is a member of `oneof` _ `artifacts` .
|
`custom_model` |
The custom model to deploy from a Google Cloud Storage URI. This field is a member of `oneof` _ `artifacts` .
|
`destination` |
`str`
Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`
|
`model_config` |
Optional. The model config to use for the deployment. If not specified, the default model config will be used. |
`endpoint_config` |
Optional. The endpoint config to use for the deployment. If not specified, the default endpoint config will be used. |
`deploy_config` |
Optional. The deploy config to use for the deployment. If not specified, the default deploy config will be used. |

## Classes

### CustomModel

`CustomModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The custom model to deploy from model weights in a Google Cloud Storage URI or Model Registry model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeployConfig

`DeployConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The deploy config to use for the deployment.

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Methods

### DeployRequest

`DeployRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.Deploy.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationSliceRequest -->

# Class GetModelEvaluationSliceRequest (1.134.0)

```
GetModelEvaluationSliceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.GetModelEvaluationSlice.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`
|

## Methods

### GetModelEvaluationSliceRequest

```
GetModelEvaluationSliceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.GetModelEvaluationSlice.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedDb.KNN -->

# Class KNN (1.134.0)

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UrlContext -->

# Class UrlContext (1.134.0)

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

## Methods

### UrlContext

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionManifest -->

# Class ExtensionManifest (1.134.0)

`ExtensionManifest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manifest spec of an Extension needed for runtime execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. Extension name shown to the LLM. The name can be up to 128 characters long. |
`description` |
`str`
Required. The natural language description shown to the LLM. It should describe the usage of the extension, and is essential for the LLM to perform reasoning. e.g., if the extension is a data store, you can let the LLM know what data it contains. |
`api_spec` |
Required. Immutable. The API specification shown to the LLM. |
`auth_config` |
Required. Immutable. Type of auth supported by this extension. |

## Classes

### ApiSpec

`ApiSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API specification shown to the LLM.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExtensionManifest

`ExtensionManifest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Manifest spec of an Extension needed for runtime execution.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchPublisherModelConfigRequest -->

# Class FetchPublisherModelConfigRequest (1.134.0)

```
FetchPublisherModelConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.FetchPublisherModelConfig.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the publisher model, in the format of `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` .
|

## Methods

### FetchPublisherModelConfigRequest

```
FetchPublisherModelConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.FetchPublisherModelConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualitySpec -->

# Class PairwiseSummarizationQualitySpec (1.134.0)

```
PairwiseSummarizationQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute pairwise summarization quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### PairwiseSummarizationQualitySpec

```
PairwiseSummarizationQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.VertexRagStore -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsRequest -->

# Class ListTensorboardExperimentsRequest (1.134.0)

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Tensorboard to list TensorboardExperiments. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`filter` |
`str`
Lists the TensorboardExperiments that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardExperiments to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardExperiments are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardExperiments call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardExperiments must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardExperimentsRequest

```
ListTensorboardExperimentsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardExperiments.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFractionSplit -->

# Class ExportFractionSplit (1.134.0)

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### ExportFractionSplit

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataOperationMetadata -->

# Class ExportDataOperationMetadata (1.134.0)

`ExportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ExportData.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`gcs_output_directory` |
`str`
A Google Cloud Storage directory which path ends with '/'. The exported data is stored in the directory. |

## Methods

### ExportDataOperationMetadata

`ExportDataOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime operation information for DatasetService.ExportData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobOutput.MultiTrialJobOutput -->

# Class MultiTrialJobOutput (1.134.0)

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

## Attributes |
|
|---|---|
Name |
Description |
`search_trials` |
`MutableSequence[`
Output only. List of NasTrials that were started as part of search stage. |
`train_trials` |
`MutableSequence[`
Output only. List of NasTrials that were started as part of train stage. |

## Methods

### MultiTrialJobOutput

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualityInput -->

# Class PairwiseQuestionAnsweringQualityInput (1.134.0)

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise question answering quality score metric. |
`instance` |
Required. Pairwise question answering quality instance. |

## Methods

### PairwiseQuestionAnsweringQualityInput

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTables -->

# Class AutoMlTables (1.134.0)

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

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

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresAsyncPager -->

# Class ListFeatureOnlineStoresAsyncPager (1.134.0)

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

## Methods

### ListFeatureOnlineStoresAsyncPager

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient -->

# Class EndpointServiceClient (1.134.0)

```
EndpointServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### EndpointServiceClient

```
EndpointServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the endpoint service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the EndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_create_endpoint)(request=request)
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
The request object. Request message for EndpointService.CreateEndpoint. |
`parent` |
`str`
Required. The resource name of the Location to create the Endpoint in. Format: |
`endpoint` |
Required. The Endpoint to create. This corresponds to the |
`endpoint_id` |
`str`
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_delete_endpoint)(request=request)
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
The request object. Request message for EndpointService.DeleteEndpoint. |
`name` |
`str`
Required. The name of the Endpoint resource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_deploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_deploy_model)(request=request)
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
The request object. Request message for EndpointService.DeployModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to deploy a Model. Format: |
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. This corresponds to the |
`traffic_split` |
`MutableMapping[str, int]`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
`EndpointServiceClient` |
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
`EndpointServiceClient` |
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
`EndpointServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_get_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EndpointService.GetEndpoint |
`name` |
`str`
Required. The name of the Endpoint resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager
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
def sample_list_endpoints():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_list_endpoints)(request=request)
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
The request object. Request message for EndpointService.ListEndpoints. |
`parent` |
`str`
Required. The resource name of the Location from which to list the Endpoints. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_mutate_deployed_model)(request=request)
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
The request object. Request message for EndpointService.MutateDeployedModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: |
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - |
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
`google.api_core.operation.Operation` |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_undeploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_undeploy_model)(request=request)
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
The request object. Request message for EndpointService.UndeployModel. |
`endpoint` |
`str`
Required. The name of the Endpoint resource from which to undeploy a Model. Format: |
`deployed_model_id` |
`str`
Required. The ID of the DeployedModel to be undeployed from the Endpoint. This corresponds to the |
`traffic_split` |
`MutableMapping[str, int]`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
google.api_core.retry.retry_unary.Retry,
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
def sample_update_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_update_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EndpointService.UpdateEndpoint. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1.
```[EndpointServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceClient_update_endpoint_long_running)(request=request)
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
The request object. Request message for EndpointService.UpdateEndpointLongRunning. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringAlertsAsyncPager -->

# Class SearchModelMonitoringAlertsAsyncPager (1.134.0)

```
SearchModelMonitoringAlertsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
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


A pager for iterating through `search_model_monitoring_alerts`

requests.

This class thinly wraps an initial
[SearchModelMonitoringAlertsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_monitoring_alerts`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelMonitoringAlerts`

requests and continue to iterate
through the `model_monitoring_alerts`

field on the
corresponding responses.

All the usual [SearchModelMonitoringAlertsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringAlertsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelMonitoringAlertsAsyncPager

```
SearchModelMonitoringAlertsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringAlertsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Examples.ExampleGcsSource -->

# Class ExampleGcsSource (1.134.0)

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

## Attributes |
|
|---|---|
Name |
Description |
`data_format` |
The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported. |
`gcs_source` |
The Cloud Storage location for the input instances. |

## Classes

### DataFormat

`DataFormat(value)`


The format of the input example instances.

## Methods

### ExampleGcsSource

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolRequest -->

# Class CreateSpecialistPoolRequest (1.134.0)

`CreateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.CreateSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent Project name for the new SpecialistPool. The form is `projects/{project}/locations/{location}` .
|
`specialist_pool` |
Required. The SpecialistPool to create. |

## Methods

### CreateSpecialistPoolRequest

`CreateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.CreateSpecialistPool.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse -->

# Class ListContextsResponse (1.134.0)

`ListContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListContexts.

## Attributes |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
The Contexts retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListContextsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListContextsResponse

`ListContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListContexts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteBatchPredictionJobRequest -->

# Class DeleteBatchPredictionJobRequest (1.134.0)

```
DeleteBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob resource to be deleted. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### DeleteBatchPredictionJobRequest

```
DeleteBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteBatchPredictionJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchImportModelEvaluationSlicesResponse -->

# Class BatchImportModelEvaluationSlicesResponse (1.134.0)

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices

## Attribute |
|
|---|---|
Name |
Description |
`imported_model_evaluation_slices` |
`MutableSequence[str]`
Output only. List of imported ModelEvaluationSlice.name. |

## Methods

### BatchImportModelEvaluationSlicesResponse

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDeploymentResourcePoolRequest -->

# Class GetDeploymentResourcePoolRequest (1.134.0)

```
GetDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for GetDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DeploymentResourcePool to retrieve. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|

## Methods

### GetDeploymentResourcePoolRequest

```
GetDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for GetDeploymentResourcePool method.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse -->

# Class ListNasTrialDetailsResponse (1.134.0)

`ListNasTrialDetailsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasTrialDetails

## Attributes |
|
|---|---|
Name |
Description |
`nas_trial_details` |
`MutableSequence[`
List of top NasTrials in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListNasTrialDetailsRequest.page_token to obtain that page. |

## Methods

### ListNasTrialDetailsResponse

`ListNasTrialDetailsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasTrialDetails

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMetadataStoreRequest -->

# Class DeleteMetadataStoreRequest (1.134.0)

`DeleteMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteMetadataStore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the MetadataStore to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`force` |
`bool`
Deprecated: Field is no longer supported. |

## Methods

### DeleteMetadataStoreRequest

`DeleteMetadataStoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteMetadataStore.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFractionSplit -->

# Class ExportFractionSplit (1.134.0)

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |

## Methods

### ExportFractionSplit

`ExportFractionSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns the input data to training, validation, and test sets as per
the given fractions. Any of `training_fraction`

,
`validation_fraction`

and `test_fraction`

may optionally be
provided, they must sum to up to 1. If the provided ones sum to less
than 1, the remainder is assigned to sets as decided by Vertex AI.
If none of the fractions are set, by default roughly 80% of data is
used for training, 10% for validation, and 10% for test.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.index_service.pagers`

module.

## Classes

[ListIndexesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesAsyncPager)

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse) object, and
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

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListIndexesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesPager)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1.types.index_service.ListIndexesResponse,
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
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse) object, and
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

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointRequest -->

# Class UpdateEndpointRequest (1.134.0)

`UpdateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UpdateEndpoint.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateEndpointRequest

`UpdateEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.UpdateEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateSpecialistPoolRequest -->

# Class UpdateSpecialistPoolRequest (1.134.0)

`UpdateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.UpdateSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. |

## Methods

### UpdateSpecialistPoolRequest

`UpdateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.UpdateSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddTrialMeasurementRequest -->

# Class AddTrialMeasurementRequest (1.134.0)

`AddTrialMeasurementRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.AddTrialMeasurement.

## Attributes |
|
|---|---|
Name |
Description |
`trial_name` |
`str`
Required. The name of the trial to add measurement. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|
`measurement` |
Required. The measurement to be added to a Trial. |

## Methods

### AddTrialMeasurementRequest

`AddTrialMeasurementRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.AddTrialMeasurement.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataResponse.TuningResourceUsageAssessmentResult -->

# Class TuningResourceUsageAssessmentResult (1.134.0)

```
TuningResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning resource usage assessment.

## Attributes |
|
|---|---|
Name |
Description |
`token_count` |
`int`
Number of tokens in the tuning dataset. |
`billable_character_count` |
`int`
Number of billable tokens in the tuning dataset. |

## Methods

### TuningResourceUsageAssessmentResult

```
TuningResourceUsageAssessmentResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The result of the tuning resource usage assessment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualitySpec -->

# Class PairwiseSummarizationQualitySpec (1.134.0)

```
PairwiseSummarizationQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute pairwise summarization quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### PairwiseSummarizationQualitySpec

```
PairwiseSummarizationQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SupervisedTuningDatasetDistribution.DatasetBucket -->

# Class DatasetBucket (1.134.0)

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Attributes |
|
|---|---|
Name |
Description |
`count` |
`float`
Output only. Number of values in the bucket. |
`left` |
`float`
Output only. Left bound of the bucket. |
`right` |
`float`
Output only. Right bound of the bucket. |

## Methods

### DatasetBucket

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager -->

# Class ListDeploymentResourcePoolsAsyncPager (1.134.0)

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse) object, and
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

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDeploymentResourcePoolsAsyncPager

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.featurestore_service.pagers`

module.

## Classes

[ListEntityTypesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesAsyncPager)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
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

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEntityTypesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesPager)

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

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesAsyncPager)

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

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesPager)

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

[ListFeaturestoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager)

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse) object, and
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

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturestoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresPager)

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

[SearchFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesAsyncPager)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
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

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec -->

# Class StudySpec (1.134.0)

`StudySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents specification of a Study.

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
`decay_curve_stopping_spec` |
The automated early stopping spec using decay curve rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`median_automated_stopping_spec` |
The automated early stopping spec using median rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`convex_automated_stopping_spec` |
The automated early stopping spec using convex stopping rule. This field is a member of `oneof` _ `automated_stopping_spec` .
|
`metrics` |
`MutableSequence[`
Required. Metric specs for the Study. |
`parameters` |
`MutableSequence[`
Required. The set of parameters to tune. |
`algorithm` |
The search algorithm specified for the Study. |
`observation_noise` |
The observation noise level of the study. Currently only supported by the Vertex AI Vizier service. Not supported by HyperparameterTuningJob or TrainingPipeline. |
`measurement_selection_type` |
Describe which measurement selection type will be used |
`study_stopping_config` |
Conditions for automated stopping of a Study. Enable automated stopping by configuring at least one condition. This field is a member of `oneof` _ `_study_stopping_config` .
|

## Classes

### Algorithm

`Algorithm(value)`


The available search algorithms for the Study.

### ConvexAutomatedStoppingSpec

`ConvexAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for ConvexAutomatedStoppingSpec. When there are enough completed trials (configured by min_measurement_count), for pending trials with enough measurements and steps, the policy first computes an overestimate of the objective value at max_num_steps according to the slope of the incomplete objective value curve. No prediction can be made if the curve is completely flat. If the overestimation is worse than the best objective value of the completed trials, this pending trial will be early-stopped, but a last measurement will be added to the pending trial with max_num_steps and predicted objective value from the autoregression model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

### MeasurementSelectionType

`MeasurementSelectionType(value)`


This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose LAST_MEASUREMENT. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose BEST_MEASUREMENT. B) Are your measurements significantly noisy and/or irreproducible? If so, BEST_MEASUREMENT will tend to be over-optimistic, and it may be better to choose LAST_MEASUREMENT. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen.

### MedianAutomatedStoppingSpec

`MedianAutomatedStoppingSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The median automated stopping rule stops a pending Trial if the Trial's best objective_value is strictly below the median 'performance' of all completed Trials reported up to the Trial's last measurement. Currently, 'performance' refers to the running average of the objective values reported by the Trial in each measurement.

### MetricSpec

`MetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a metric to optimize.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ObservationNoise

`ObservationNoise(value)`


Describes the noise level of the repeated observations.

"Noisy" means that the repeated observations with the same Trial parameters may lead to different metric evaluations.

### ParameterSpec

`ParameterSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single parameter to optimize.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### StudyStoppingConfig

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

## Methods

### StudySpec

`StudySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents specification of a Study.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.PhishBlockThreshold -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service -->

# Package feature_online_store_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_online_store_service`

package.

## Classes

[FeatureOnlineStoreServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceAsyncClient)

A service for fetching feature values from the online store.

[FeatureOnlineStoreServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_service.FeatureOnlineStoreServiceClient)

A service for fetching feature values from the online store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobOutput.MultiTrialJobOutput -->

# Class MultiTrialJobOutput (1.134.0)

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

## Attributes |
|
|---|---|
Name |
Description |
`search_trials` |
`MutableSequence[`
Output only. List of NasTrials that were started as part of search stage. |
`train_trials` |
`MutableSequence[`
Output only. List of NasTrials that were started as part of train stage. |

## Methods

### MultiTrialJobOutput

`MultiTrialJobOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The output of a multi-trial Neural Architecture Search (NAS) jobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.vertex_rag_data_service.pagers`

module.

## Classes

[ListRagCorporaAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
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

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagCorporaPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagCorporaPager)

```
ListRagCorporaPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagCorporaResponse,
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
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse) object, and
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

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagFilesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager)

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

[ListRagFilesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesPager)

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse) object, and
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

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventMetadata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Examples.ExampleGcsSource -->

# Class ExampleGcsSource (1.134.0)

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

## Attributes |
|
|---|---|
Name |
Description |
`data_format` |
The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported. |
`gcs_source` |
The Cloud Storage location for the input instances. |

## Classes

### DataFormat

`DataFormat(value)`


The format of the input example instances.

## Methods

### ExampleGcsSource

`ExampleGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage input instances.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceOperationMetadata -->

# Class UpdatePersistentResourceOperationMetadata (1.134.0)

```
UpdatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Update LRO |

## Methods

### UpdatePersistentResourceOperationMetadata

```
UpdatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update PersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceOperationMetadata -->

# Class RebootPersistentResourceOperationMetadata (1.134.0)

```
RebootPersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform reboot PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Reboot LRO |

## Methods

### RebootPersistentResourceOperationMetadata

```
RebootPersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform reboot PersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceOperationMetadata -->

# Class CreatePersistentResourceOperationMetadata (1.134.0)

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Create LRO |

## Methods

### CreatePersistentResourceOperationMetadata

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse -->

# Class ListArtifactsResponse (1.134.0)

`ListArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifacts retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListArtifactsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListArtifactsResponse

`ListArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListArtifacts.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeRequest -->

# Class GetNotebookRuntimeRequest (1.134.0)

`GetNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.GetNotebookRuntime

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### GetNotebookRuntimeRequest

`GetNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.GetNotebookRuntime

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.BatchPredictionResourceUsageAssessmentConfig -->

# Class BatchPredictionResourceUsageAssessmentConfig (1.134.0)

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. The name of the model used for batch prediction. |

## Methods

### BatchPredictionResourceUsageAssessmentConfig

```
BatchPredictionResourceUsageAssessmentConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration for the batch prediction resource usage assessment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInput -->

# Class PairwiseQuestionAnsweringQualityInput (1.134.0)

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise question answering quality score metric. |
`instance` |
Required. Pairwise question answering quality instance. |

## Methods

### PairwiseQuestionAnsweringQualityInput

```
PairwiseQuestionAnsweringQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise question answering quality metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse -->

# Class ListNasTrialDetailsResponse (1.134.0)

`ListNasTrialDetailsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasTrialDetails

## Attributes |
|
|---|---|
Name |
Description |
`nas_trial_details` |
`MutableSequence[`
List of top NasTrials in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListNasTrialDetailsRequest.page_token to obtain that page. |

## Methods

### ListNasTrialDetailsResponse

`ListNasTrialDetailsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListNasTrialDetails

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse -->

# Class ListExampleStoresResponse (1.134.0)

`ListExampleStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.ListExampleStores.

## Attributes |
|
|---|---|
Name |
Description |
`example_stores` |
`MutableSequence[`
List of ExampleStore in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListExampleStoresRequest.page_token to obtain that page. |

## Methods

### ListExampleStoresResponse

`ListExampleStoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExampleStoreService.ListExampleStores.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig.LayoutParser -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.PhishBlockThreshold -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Bigtable.BigtableMetadata -->

# Class BigtableMetadata (1.134.0)

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Attributes |
|
|---|---|
Name |
Description |
`tenant_project_id` |
`str`
Tenant project ID. |
`instance_id` |
`str`
The Cloud Bigtable instance id. |
`table_id` |
`str`
The Cloud Bigtable table id. |

## Methods

### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesResponse -->

# Class BatchImportModelEvaluationSlicesResponse (1.134.0)

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices

## Attribute |
|
|---|---|
Name |
Description |
`imported_model_evaluation_slices` |
`MutableSequence[str]`
Output only. List of imported ModelEvaluationSlice.name. |

## Methods

### BatchImportModelEvaluationSlicesResponse

```
BatchImportModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.BatchImportModelEvaluationSlices

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec -->

# Class ReasoningEngineSpec (1.134.0)

`ReasoningEngineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine configurations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`source_code_spec` |
Deploy from source code files with a defined entrypoint. This field is a member of `oneof` _ `deployment_source` .
|
`service_account` |
`str`
Optional. The service account that the Reasoning Engine artifact runs as. It should have "roles/storage.objectViewer" for reading the user project's Cloud Storage and "roles/aiplatform.user" for using Vertex extensions. If not specified, the Vertex AI Reasoning Engine Service Agent in the project will be used. This field is a member of `oneof` _ `_service_account` .
|
`package_spec` |
Optional. User provided package spec of the ReasoningEngine. Ignored when users directly specify a deployment image through `deployment_spec.first_party_image_override` , but
keeping the field_behavior to avoid introducing breaking
changes. The `deployment_source` field should not be set
if `package_spec` is specified.
|
`deployment_spec` |
Optional. The specification of a Reasoning Engine deployment. |
`class_methods` |
`MutableSequence[google.protobuf.struct_pb2.Struct]`
Optional. Declarations for object class methods in OpenAPI specification format. |
`agent_framework` |
`str`
Optional. The OSS agent framework used to develop the agent. Currently supported values: "google-adk", "langchain", "langgraph", "ag2", "llama-index", "custom". |

## Classes

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PackageSpec

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.

### SourceCodeSpec

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ReasoningEngineSpec

`ReasoningEngineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine configurations

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateSpecialistPoolRequest -->

# Class UpdateSpecialistPoolRequest (1.134.0)

`UpdateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.UpdateSpecialistPool.

## Attributes |
|
|---|---|
Name |
Description |
`specialist_pool` |
Required. The SpecialistPool which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. |

## Methods

### UpdateSpecialistPoolRequest

`UpdateSpecialistPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SpecialistPoolService.UpdateSpecialistPool.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedIndexOperationMetadata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager -->

# Class ListModelDeploymentMonitoringJobsAsyncPager (1.134.0)

```
ListModelDeploymentMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse) object, and
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

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelDeploymentMonitoringJobsAsyncPager

```
ListModelDeploymentMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportModelEvaluationRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelMonitorRequest -->

# Class UpdateModelMonitorRequest (1.134.0)

`UpdateModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.UpdateModelMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`model_monitor` |
Required. The model monitoring configuration which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Mask specifying which fields to update. |

## Methods

### UpdateModelMonitorRequest

`UpdateModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.UpdateModelMonitor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataRequest -->

# Class ExportTensorboardTimeSeriesDataRequest (1.134.0)

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to export data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`filter` |
`str`
Exports the TensorboardTimeSeries' data that match the filter expression. |
`page_size` |
`int`
The maximum number of data points to return per page. The default page_size is 1000. Values must be between 1 and 10000. Values above 10000 are coerced to 10000. |
`page_token` |
`str`
A page token, received from a previous ExportTensorboardTimeSeriesData call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to ExportTensorboardTimeSeriesData must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the TensorboardTimeSeries' data. By default, TensorboardTimeSeries' data is returned in a pseudo random order. |

## Methods

### ExportTensorboardTimeSeriesDataRequest

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig.SimilaritySearchConfig -->

# Class SimilaritySearchConfig (1.134.0)

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.

## Attribute |
|
|---|---|
Name |
Description |
`embedding_model` |
`str`
Required. The model used to generate embeddings to lookup similar memories. Format: `projects/{project}/locations/{location}/publishers/google/models/{model}` .
|

## Methods

### SimilaritySearchConfig

`SimilaritySearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for how to perform similarity search on memories.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SupervisedTuningDatasetDistribution.DatasetBucket -->

# Class DatasetBucket (1.134.0)

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Attributes |
|
|---|---|
Name |
Description |
`count` |
`float`
Output only. Number of values in the bucket. |
`left` |
`float`
Output only. Left bound of the bucket. |
`right` |
`float`
Output only. Right bound of the bucket. |

## Methods

### DatasetBucket

`DatasetBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint.TypedValue -->

# Class TypedValue (1.134.0)

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

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
`double_value` |
`float`
Double. This field is a member of `oneof` _ `value` .
|
`distribution_value` |
Distribution. This field is a member of `oneof` _ `value` .
|

## Classes

### DistributionDataValue

`DistributionDataValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary statistics for a population of values.

## Methods

### TypedValue

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec -->

# Class ReasoningEngineSpec (1.134.0)

`ReasoningEngineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine configurations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`source_code_spec` |
Deploy from source code files with a defined entrypoint. This field is a member of `oneof` _ `deployment_source` .
|
`service_account` |
`str`
Optional. The service account that the Reasoning Engine artifact runs as. It should have "roles/storage.objectViewer" for reading the user project's Cloud Storage and "roles/aiplatform.user" for using Vertex extensions. If not specified, the Vertex AI Reasoning Engine Service Agent in the project will be used. This field is a member of `oneof` _ `_service_account` .
|
`package_spec` |
Optional. User provided package spec of the ReasoningEngine. Ignored when users directly specify a deployment image through `deployment_spec.first_party_image_override` , but
keeping the field_behavior to avoid introducing breaking
changes. The `deployment_source` field should not be set
if `package_spec` is specified.
|
`deployment_spec` |
Optional. The specification of a Reasoning Engine deployment. |
`class_methods` |
`MutableSequence[google.protobuf.struct_pb2.Struct]`
Optional. Declarations for object class methods in OpenAPI specification format. |
`agent_framework` |
`str`
Optional. The OSS agent framework used to develop the agent. Currently supported values: "google-adk", "langchain", "langgraph", "ag2", "llama-index", "custom". |

## Classes

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### PackageSpec

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.

### SourceCodeSpec

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ReasoningEngineSpec

`ReasoningEngineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine configurations

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ExportTensorboardTimeSeriesDataAsyncPager -->

# Class ExportTensorboardTimeSeriesDataAsyncPager (1.134.0)

```
ExportTensorboardTimeSeriesDataAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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


A pager for iterating through `export_tensorboard_time_series_data`

requests.

This class thinly wraps an initial
[ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse) object, and
provides an `__aiter__`

method to iterate through its
`time_series_data_points`

field.

If there are more pages, the `__aiter__`

method will make additional
`ExportTensorboardTimeSeriesData`

requests and continue to iterate
through the `time_series_data_points`

field on the
corresponding responses.

All the usual [ExportTensorboardTimeSeriesDataResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ExportTensorboardTimeSeriesDataAsyncPager

```
ExportTensorboardTimeSeriesDataAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ExportTensorboardTimeSeriesDataResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageSegmentationPredictionResult -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureStatsAnomaly -->

# Class FeatureStatsAnomaly (1.134.0)

`FeatureStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated at specific timestamp for specific Feature. The start_time and end_time are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, start_time = end_time. Timestamp of the stats and anomalies always refers to end_time. Raw stats and anomalies are stored in stats_uri or anomaly_uri in the tensorflow defined protos. Field data_stats contains almost identical information with the raw stats in Vertex AI defined proto, for UI to display.

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Feature importance score, only populated when cross-feature monitoring is enabled. For now only used to represent feature attribution score within range [0, 1] for ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_SKEW and ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_DRIFT. |
`stats_uri` |
`str`
Path of the stats file for current feature values in Cloud Storage bucket. Format: gs:// |
`anomaly_uri` |
`str`
Path of the anomaly file for current feature values in Cloud Storage bucket. Format: gs:// |
`distribution_deviation` |
`float`
Deviation from the current stats to baseline stats. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. |
`anomaly_detection_threshold` |
`float`
This is the threshold used when detecting anomalies. The threshold can be changed by user, so this one might be different from ThresholdConfig.value. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The start timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), start_time is only used to indicate the monitoring intervals, so it always equals to (end_time - monitoring_interval). |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The end timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), end_time indicates the timestamp of the data used to generate stats (e.g. timestamp we take snapshots for feature values). |

## Methods

### FeatureStatsAnomaly

`FeatureStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated at specific timestamp for specific Feature. The start_time and end_time are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, start_time = end_time. Timestamp of the stats and anomalies always refers to end_time. Raw stats and anomalies are stored in stats_uri or anomaly_uri in the tensorflow defined protos. Field data_stats contains almost identical information with the raw stats in Vertex AI defined proto, for UI to display.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPersistentResourceRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileResponse -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateFetchAccessTokenResponse -->

# Class GenerateFetchAccessTokenResponse (1.134.0)

```
GenerateFetchAccessTokenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.GenerateFetchAccessToken.

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


Response message for FeatureOnlineStoreService.GenerateFetchAccessToken.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardExperimentRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateFetchAccessTokenRequest -->

# Class GenerateFetchAccessTokenRequest (1.134.0)

```
GenerateFetchAccessTokenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreService.GenerateFetchAccessToken.

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


Request message for FeatureOnlineStoreService.GenerateFetchAccessToken.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse -->

# Class ListArtifactsResponse (1.134.0)

`ListArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifacts retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListArtifactsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListArtifactsResponse

`ListArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListArtifacts.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceOperationMetadata -->

# Class UpdatePersistentResourceOperationMetadata (1.134.0)

```
UpdatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Update LRO |

## Methods

### UpdatePersistentResourceOperationMetadata

```
UpdatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform update PersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelectionConfig -->

# Class FeatureSelectionConfig (1.134.0)

`FeatureSelectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature selection configuration for the FeatureMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`feature_configs` |
`MutableSequence[`
Optional. A list of features to be monitored and each feature's drift threshold. |

## Classes

### FeatureConfig

`FeatureConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature configuration.

## Methods

### FeatureSelectionConfig

`FeatureSelectionConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature selection configuration for the FeatureMonitor.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceOperationMetadata -->

# Class RebootPersistentResourceOperationMetadata (1.134.0)

```
RebootPersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform reboot PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Reboot LRO |

## Methods

### RebootPersistentResourceOperationMetadata

```
RebootPersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform reboot PersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse -->

# Class ListModelMonitorsResponse (1.134.0)

`ListModelMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelMonitoringService.ListModelMonitors

## Attributes |
|
|---|---|
Name |
Description |
`model_monitors` |
`MutableSequence[`
List of ModelMonitor in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListModelMonitorsRequest.page_token to obtain that page. |

## Methods

### ListModelMonitorsResponse

`ListModelMonitorsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelMonitoringService.ListModelMonitors

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeRequest -->

# Class GetNotebookRuntimeRequest (1.134.0)

`GetNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.GetNotebookRuntime

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### GetNotebookRuntimeRequest

`GetNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.GetNotebookRuntime

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureStatsAnomaly -->

# Class FeatureStatsAnomaly (1.134.0)

`FeatureStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated at specific timestamp for specific Feature. The start_time and end_time are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, start_time = end_time. Timestamp of the stats and anomalies always refers to end_time. Raw stats and anomalies are stored in stats_uri or anomaly_uri in the tensorflow defined protos. Field data_stats contains almost identical information with the raw stats in Vertex AI defined proto, for UI to display.

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Feature importance score, only populated when cross-feature monitoring is enabled. For now only used to represent feature attribution score within range [0, 1] for ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_SKEW and ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_DRIFT. |
`stats_uri` |
`str`
Path of the stats file for current feature values in Cloud Storage bucket. Format: gs:// |
`anomaly_uri` |
`str`
Path of the anomaly file for current feature values in Cloud Storage bucket. Format: gs:// |
`distribution_deviation` |
`float`
Deviation from the current stats to baseline stats. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. |
`anomaly_detection_threshold` |
`float`
This is the threshold used when detecting anomalies. The threshold can be changed by user, so this one might be different from ThresholdConfig.value. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The start timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), start_time is only used to indicate the monitoring intervals, so it always equals to (end_time - monitoring_interval). |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The end timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), end_time indicates the timestamp of the data used to generate stats (e.g. timestamp we take snapshots for feature values). |

## Methods

### FeatureStatsAnomaly

`FeatureStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats and Anomaly generated at specific timestamp for specific Feature. The start_time and end_time are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, start_time = end_time. Timestamp of the stats and anomalies always refers to end_time. Raw stats and anomalies are stored in stats_uri or anomaly_uri in the tensorflow defined protos. Field data_stats contains almost identical information with the raw stats in Vertex AI defined proto, for UI to display.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceOperationMetadata -->

# Class CreatePersistentResourceOperationMetadata (1.134.0)

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for PersistentResource. |
`progress_message` |
`str`
Progress Message for Create LRO |

## Methods

### CreatePersistentResourceOperationMetadata

```
CreatePersistentResourceOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform create PersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTables -->

# Class AutoMlTables (1.134.0)

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

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

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

### AutoMlTables

`AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Tables Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualityInstance -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Bigtable.BigtableMetadata -->

# Class BigtableMetadata (1.134.0)

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

## Attributes |
|
|---|---|
Name |
Description |
`tenant_project_id` |
`str`
Tenant project ID. |
`instance_id` |
`str`
The Cloud Bigtable instance id. |
`table_id` |
`str`
The Cloud Bigtable table id. |

## Methods

### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the Bigtable instance. This is used by direct read access to the Bigtable in tenant project.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CachedContent.UsageMetadata -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetHyperparameterTuningJobRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelectionConfig.FeatureConfig -->

# Class FeatureConfig (1.134.0)

`FeatureConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature configuration.

## Attributes |
|
|---|---|
Name |
Description |
`feature_id` |
`str`
Required. The ID of the feature resource. Final component of the Feature's resource name. |
`drift_threshold` |
`float`
Optional. Drift threshold. If calculated difference with baseline data larger than threshold, it will be considered as the feature has drift. If not present, the threshold will be default to 0.3. |

## Methods

### FeatureConfig

`FeatureConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature configuration.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportTensorboardTimeSeriesDataRequest -->

# Class ExportTensorboardTimeSeriesDataRequest (1.134.0)

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to export data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`filter` |
`str`
Exports the TensorboardTimeSeries' data that match the filter expression. |
`page_size` |
`int`
The maximum number of data points to return per page. The default page_size is 1000. Values must be between 1 and 10000. Values above 10000 are coerced to 10000. |
`page_token` |
`str`
A page token, received from a previous ExportTensorboardTimeSeriesData call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to ExportTensorboardTimeSeriesData must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the TensorboardTimeSeries' data. By default, TensorboardTimeSeries' data is returned in a pseudo random order. |

## Methods

### ExportTensorboardTimeSeriesDataRequest

```
ExportTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ExportTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint -->

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
