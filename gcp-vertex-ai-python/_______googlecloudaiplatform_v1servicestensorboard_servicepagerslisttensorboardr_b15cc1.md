---
merged_at: 2026-01-25T21:47:44.390360
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardru_fd870c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrun_50c71e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardruns_0887d5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrunsa_51ea99.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrunsas_1ed672.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrunsasy_816c0f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrunsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsAsyncPager -->

# Class ListTensorboardRunsAsyncPager (1.134.0)

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
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


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__aiter__`

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

### ListTensorboardRunsAsyncPager

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookexecutionjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsPager -->

# Class ListNotebookExecutionJobsPager (1.134.0)

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__iter__`

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

### ListNotebookExecutionJobsPager

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetversionsas_e76e39.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetversionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsAsyncPager -->

# Class ListDatasetVersionsAsyncPager (1.134.0)

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__aiter__`

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

### ListDatasetVersionsAsyncPager

```
ListDatasetVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessuggesttrialsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsRequest -->

# Class SuggestTrialsRequest (1.134.0)

`SuggestTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.SuggestTrials.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The project and location that the Study belongs to. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`suggestion_count` |
`int`
Required. The number of suggestions requested. It must be positive. |
`client_id` |
`str`
Required. The identifier of the client that is requesting the suggestion. If multiple SuggestTrialsRequests have the same `client_id` , the service will return the identical
suggested Trial if the Trial is pending, and provide a new
Trial if the last suggested Trial was completed.
|
`contexts` |
`MutableSequence[`
Optional. This allows you to specify the "context" for a Trial; a context is a slice (a subspace) of the search space. Typical uses for contexts: 1) You are using Vizier to tune a server for best performance, but there's a strong weekly cycle. The context specifies the day-of-week. This allows Tuesday to generalize from Wednesday without assuming that everything is identical. 2) Imagine you're optimizing some medical treatment for people. As they walk in the door, you know certain facts about them (e.g. sex, weight, height, blood-pressure). Put that information in the context, and Vizier will adapt its suggestions to the patient. 3) You want to do a fair A/B test efficiently. Specify the "A" and "B" conditions as contexts, and Vizier will generalize between "A" and "B" conditions. If they are similar, this will allow Vizier to converge to the optimum faster than if "A" and "B" were separate Studies. NOTE: You can also enter contexts as REQUESTED Trials, e.g. via the CreateTrial() RPC; that's the asynchronous option where you don't need a close association between contexts and suggestions. NOTE: All the Parameters you set in a context MUST be defined in the Study. NOTE: You must supply 0 or $suggestion_count contexts. If you don't supply any contexts, Vizier will make suggestions from the full search space specified in the StudySpec; if you supply a full set of context, each suggestion will match the corresponding context. NOTE: A Context with no features set matches anything, and allows suggestions from the full search space. NOTE: Contexts MUST lie within the search space specified in the StudySpec. It's an error if they don't. NOTE: Contexts preferentially match ACTIVE then REQUESTED trials before new suggestions are generated. NOTE: Generation of suggestions involves a match between a Context and (optionally) a REQUESTED trial; if that match is not fully specified, a suggestion will be geneated in the merged subspace. |

## Methods

### SuggestTrialsRequest

`SuggestTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.SuggestTrials.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesextension_registry_servicepagerslistexten_4d97de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesextension_registry_servicepagerslistextens_de638c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_registry_servicepagerslistextensionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsAsyncPager -->

# Class ListExtensionsAsyncPager (1.134.0)

```
ListExtensionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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


A pager for iterating through `list_extensions`

requests.

This class thinly wraps an initial
[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`extensions`

field.

If there are more pages, the `__aiter__`

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

### ListExtensionsAsyncPager

```
ListExtensionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisesummarizationqualityresult_googlecloudaipl_7d0e02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisesummarizationqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualityResult -->

# Class PairwiseSummarizationQualityResult (1.134.0)

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise summarization prediction choice. |
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseSummarizationQualityResult

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadFeatureValuesResponse -->

# Class ReadFeatureValuesResponse (1.134.0)

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`header` |
Response header. |
`entity_view` |
Entity view with Feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested. |

## Classes

### EntityView

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Methods

### ReadFeatureValuesResponse

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmigration_servicepagerssearchmigratableresource_2e3ef6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmigration_servicepagerssearchmigratableresourcespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesPager -->

# Class SearchMigratableResourcesPager (1.134.0)

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

## Methods

### SearchMigratableResourcesPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeminitemplateconfig_googlecloudaiplatform_v1_e61c7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeminitemplateconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GeminiTemplateConfig -->

# Class GeminiTemplateConfig (1.134.0)

`GeminiTemplateConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Template configuration to create Gemini examples from a multimodal dataset.

## Attributes |
|
|---|---|
Name |
Description |
`gemini_example` |
Required. The template that will be used for assembling the request to use for downstream applications. |
`field_mapping` |
`MutableMapping[str, str]`
Required. Map of template parameters to the columns in the dataset table. |

## Classes

### FieldMappingEntry

`FieldMappingEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### GeminiTemplateConfig

`GeminiTemplateConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Template configuration to create Gemini examples from a multimodal dataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeatureviewrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureViewRequest -->

# Class CreateFeatureViewRequest (1.134.0)

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`feature_view` |
Required. The FeatureView to create. |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a FeatureOnlineStore.
|
`run_sync_immediately` |
`bool`
Immutable. If set to true, one on demand sync will be run immediately, regardless whether the FeatureView.sync_config is configured or not. |

## Methods

### CreateFeatureViewRequest

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagers_38a05c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagersl_b733de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagersli_f0c8c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagerslistfeatureviewspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager -->

# Class ListFeatureViewsPager (1.134.0)

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

## Methods

### ListFeatureViewsPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesaddcontextartifactsandexecutionsrequest_googl_f93bef.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesaddcontextartifactsandexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextArtifactsAndExecutionsRequest -->

# Class AddContextArtifactsAndExecutionsRequest (1.134.0)

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`artifacts` |
`MutableSequence[str]`
The resource names of the Artifacts to attribute to the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`executions` |
`MutableSequence[str]`
The resource names of the Executions to associate with the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### AddContextArtifactsAndExecutionsRequest

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelsourceinfomodelsourcetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelSourceInfo.ModelSourceType -->

# Class ModelSourceType (1.134.0)

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_SOURCE_TYPE_UNSPECIFIED` |
Should not be used. |
`AUTOML` |
The Model is uploaded by automl training pipeline. |
`CUSTOM` |
The Model is uploaded by user or custom training pipeline. |
`BQML` |
The Model is registered and sync'ed from BigQuery ML. |
`MODEL_GARDEN` |
The Model is saved or tuned from Model Garden. |
`GENIE` |
The Model is saved or tuned from Genie. |
`CUSTOM_TEXT_EMBEDDING` |
The Model is uploaded by text embedding finetuning pipeline. |
`MARKETPLACE` |
The Model is saved or tuned from Marketplace. |

## Methods

### ModelSourceType

`ModelSourceType(value)`


Source of the model. Different from `objective`

field, this
`ModelSourceType`

enum indicates the source from which the model
was accessed or obtained, whereas the `objective`

indicates the
overall aim or function of this model.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreadfeaturevaluesresponse_googlecloudaiplatform_v_f15c3a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadfeaturevaluesresponse_googlecloudaiplatform_v1_2319a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadfeaturevaluesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadFeatureValuesResponse -->

# Class ReadFeatureValuesResponse (1.134.0)

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`header` |
Response header. |
`entity_view` |
Entity view with Feature values. This may be the entity in the Featurestore if values for all Features were requested, or a projection of the entity in the Featurestore if values for only some Features were requested. |

## Classes

### EntityView

`EntityView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Entity view with Feature values.

### FeatureDescriptor

`FeatureDescriptor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for requested Features.

### Header

`Header(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response header with metadata for the requested ReadFeatureValuesRequest.entity_type and Features.

## Methods

### ReadFeatureValuesResponse

`ReadFeatureValuesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreOnlineServingService.ReadFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturevaluesresponseselecttimerangeandfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesResponse.SelectTimeRangeAndFeature -->

# Class SelectTimeRangeAndFeature (1.134.0)

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.

## Attributes |
|
|---|---|
Name |
Description |
`impacted_feature_count` |
`int`
The count of the features or columns impacted. This is the same as the feature count in the request. |
`offline_storage_modified_entity_row_count` |
`int`
The count of modified entity rows in the offline storage. Each row corresponds to the combination of an entity ID and a timestamp. One entity ID can have multiple rows in the offline storage. Within each row, only the features specified in the request are deleted. |
`online_storage_modified_entity_count` |
`int`
The count of modified entities in the online storage. Each entity ID corresponds to one entity. Within each entity, only the features specified in the request are deleted. |

## Methods

### SelectTimeRangeAndFeature

`SelectTimeRangeAndFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message if the request uses the SelectTimeRangeAndFeature option.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadatastoresasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataStoresAsyncPager -->

# Class ListMetadataStoresAsyncPager (1.134.0)

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse) object, and
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

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataStoresAsyncPager

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataStoresResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesindex_endpoint_servicepagerslistindexendpoints_1ba16c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_endpoint_servicepagerslistindexendpointsa_7a4263.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_endpoint_servicepagerslistindexendpointsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager -->

# Class ListIndexEndpointsAsyncPager (1.134.0)

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__aiter__`

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

### ListIndexEndpointsAsyncPager

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_servicepagerslistreasoningenginespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesPager -->

# Class ListReasoningEnginesPager (1.134.0)

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse) object, and
provides an `__iter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__iter__`

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

### ListReasoningEnginesPager

```
ListReasoningEnginesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadataschemasa_0d76a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistmetadataschemasasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager -->

# Class ListMetadataSchemasAsyncPager (1.134.0)

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse) object, and
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

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMetadataSchemasAsyncPager

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListMetadataSchemasResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessuggesttrialsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsRequest -->

# Class SuggestTrialsRequest (1.134.0)

`SuggestTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.SuggestTrials.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The project and location that the Study belongs to. Format: `projects/{project}/locations/{location}/studies/{study}`
|
`suggestion_count` |
`int`
Required. The number of suggestions requested. It must be positive. |
`client_id` |
`str`
Required. The identifier of the client that is requesting the suggestion. If multiple SuggestTrialsRequests have the same `client_id` , the service will return the identical
suggested Trial if the Trial is pending, and provide a new
Trial if the last suggested Trial was completed.
|
`contexts` |
`MutableSequence[`
Optional. This allows you to specify the "context" for a Trial; a context is a slice (a subspace) of the search space. Typical uses for contexts: 1) You are using Vizier to tune a server for best performance, but there's a strong weekly cycle. The context specifies the day-of-week. This allows Tuesday to generalize from Wednesday without assuming that everything is identical. 2) Imagine you're optimizing some medical treatment for people. As they walk in the door, you know certain facts about them (e.g. sex, weight, height, blood-pressure). Put that information in the context, and Vizier will adapt its suggestions to the patient. 3) You want to do a fair A/B test efficiently. Specify the "A" and "B" conditions as contexts, and Vizier will generalize between "A" and "B" conditions. If they are similar, this will allow Vizier to converge to the optimum faster than if "A" and "B" were separate Studies. NOTE: You can also enter contexts as REQUESTED Trials, e.g. via the CreateTrial() RPC; that's the asynchronous option where you don't need a close association between contexts and suggestions. NOTE: All the Parameters you set in a context MUST be defined in the Study. NOTE: You must supply 0 or $suggestion_count contexts. If you don't supply any contexts, Vizier will make suggestions from the full search space specified in the StudySpec; if you supply a full set of context, each suggestion will match the corresponding context. NOTE: A Context with no features set matches anything, and allows suggestions from the full search space. NOTE: Contexts MUST lie within the search space specified in the StudySpec. It's an error if they don't. NOTE: Contexts preferentially match ACTIVE then REQUESTED trials before new suggestions are generated. NOTE: Generation of suggestions involves a match between a Context and (optionally) a REQUESTED trial; if that match is not fully specified, a suggestion will be geneated in the merged subspace. |

## Methods

### SuggestTrialsRequest

`SuggestTrialsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.SuggestTrials.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmatch_servicematchserviceclient_____google_d2ed85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmatch_servicematchserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.134.0)

```
MatchServiceClient(
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
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
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
google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsRequest,
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
def sample_find_neighbors():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_find_neighbors)(request=request)
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
google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsRequest,
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
def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceClient_read_index_datapoints)(request=request)
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typestrajectoryrecallinstance_googlecloudaiplat_fb3c0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typestrajectoryrecallinstance_googlecloudaiplatf_f7726c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typestrajectoryrecallinstance_googlecloudaiplatfo_829b8c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestrajectoryrecallinstance_googlecloudaiplatfor_171e1d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryrecallinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryRecallInstance -->

# Class TrajectoryRecallInstance (1.134.0)

`TrajectoryRecallInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall instance.

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

### TrajectoryRecallInstance

`TrajectoryRecallInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryRecall instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespairwisesummarizationqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityResult -->

# Class PairwiseSummarizationQualityResult (1.134.0)

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise summarization prediction choice. |
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseSummarizationQualityResult

```
PairwiseSummarizationQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesimportdataresponse_googlecloudaiplatform_v1beta1t_9aaabe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesimportdataresponse_googlecloudaiplatform_v1beta1ty_975312.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesimportdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportDataResponse -->

# Class ImportDataResponse (1.134.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataResponse -->

# Class ImportDataResponse (1.134.0)

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.

## Methods

### ImportDataResponse

`ImportDataResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ImportData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprivateendpoints.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrivateEndpoints -->

# Class PrivateEndpoints (1.134.0)

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.

## Attributes |
|
|---|---|
Name |
Description |
`predict_http_uri` |
`str`
Output only. Http(s) path to send prediction requests. |
`explain_http_uri` |
`str`
Output only. Http(s) path to send explain requests. |
`health_http_uri` |
`str`
Output only. Http(s) path to send health check requests. |
`service_attachment` |
`str`
Output only. The name of the service attachment resource. Populated if private service connect is enabled. |

## Methods

### PrivateEndpoints

`PrivateEndpoints(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predict_http_uri, explain_http_uri or health_http_uri. To send request via private service connect, use service_attachment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturestore_48b1de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturestoresasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager -->

# Class ListFeaturestoresAsyncPager (1.134.0)

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

## Methods

### ListFeaturestoresAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistdatalabelingjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsAsyncPager -->

# Class ListDataLabelingJobsAsyncPager (1.134.0)

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse) object, and
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

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataLabelingJobsAsyncPager

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesartifact_googlecloudaiplatform_v1servicestensorbo_2ad45b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesartifact_googlecloudaiplatform_v1servicestensorboa_eee851.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesartifact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Artifact -->

# Class Artifact (1.134.0)

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Artifact. |
`display_name` |
`str`
User provided display name of the Artifact. May be up to 128 Unicode characters. |
`uri` |
`str`
The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was last updated. |
`state` |
The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Artifact |

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

### State

`State(value)`


Describes the state of the Artifact.

## Methods

### Artifact

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardexperimentspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager -->

# Class ListTensorboardExperimentsPager (1.134.0)

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse) object, and
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

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsPager

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploydeploymetada_544f33.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploydeploymetadat_abcdaf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoactiondeploydeploymetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction.Deploy.DeployMetadata -->

# Class DeployMetadata (1.134.0)

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.

## Attributes |
|
|---|---|
Name |
Description |
`labels` |
`MutableMapping[str, str]`
Optional. Labels for the deployment config. For managing deployment config like verifying, source of deployment config, etc. |
`sample_request` |
`str`
Optional. Sample request for deployed endpoint. |

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

### DeployMetadata

`DeployMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata information about the deployment for managing deployment config.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborsearchoperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata -->

# Class NearestNeighborSearchOperationMetadata (1.134.0)

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.

## Attributes |
|
|---|---|
Name |
Description |
`content_validation_stats` |
`MutableSequence[`
The validation stats of the content (per file) to be inserted or updated on the Matching Engine Index resource. Populated if contentsDeltaUri is provided as part of Index.metadata. Please note that, currently for those files that are broken or has unsupported file format, we will not have the stats for those files. |
`data_bytes_count` |
`int`
The ingested data size in bytes. |

## Classes

### ContentValidationStats

`ContentValidationStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### NearestNeighborSearchOperationMetadata

```
NearestNeighborSearchOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation metadata with regard to Matching Engine Index.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesenterprisewebsearch_googlecloudaiplatform_v1typese_2ea23f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesenterprisewebsearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EnterpriseWebSearch -->

# Class EnterpriseWebSearch (1.134.0)

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### EnterpriseWebSearch

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeserroranalysisannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ErrorAnalysisAnnotation -->

# Class ErrorAnalysisAnnotation (1.134.0)

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

## Attributes |
|
|---|---|
Name |
Description |
`attributed_items` |
`MutableSequence[`
Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type. |
`query_type` |
The query type used for finding the attributed items. |
`outlier_score` |
`float`
The outlier score of this annotated item. Usually defined as the min of all distances from attributed items. |
`outlier_threshold` |
`float`
The threshold used to determine if this annotation is an outlier or not. |

## Classes

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

### QueryType

`QueryType(value)`


The query type used for finding the attributed items.

## Methods

### ErrorAnalysisAnnotation

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_g_557200.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_go_a4bd0c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_goo_01e9c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_goog_105e88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_googl_f80e9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec_google_17e5e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecsourcecodespecpythonspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec.PythonSpec -->

# Class PythonSpec (1.134.0)

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Attributes |
|
|---|---|
Name |
Description |
`version` |
`str`
Optional. The version of Python to use. Support version includes 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, default value is 3.10. |
`entrypoint_module` |
`str`
Optional. The Python module to load as the entrypoint, specified as a fully qualified module name. For example: path.to.agent. If not specified, defaults to "agent". The project root will be added to Python sys.path, allowing imports to be specified relative to the root. |
`entrypoint_object` |
`str`
Optional. The name of the callable object within the `entrypoint_module` to use as the application If not
specified, defaults to "root_agent".
|
`requirements_file` |
`str`
Optional. The path to the requirements file, relative to the source root. If not specified, defaults to "requirements.txt". |

## Methods

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitormodelmonitoringtarget.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitor.ModelMonitoringTarget -->

# Class ModelMonitoringTarget (1.134.0)

`ModelMonitoringTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The monitoring target refers to the entity that is subject to analysis. e.g. Vertex AI Model version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`vertex_model` |
Model in Vertex AI Model Registry. This field is a member of `oneof` _ `source` .
|

## Classes

### VertexModelSource

`VertexModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model in Vertex AI Model Registry.

## Methods

### ModelMonitoringTarget

`ModelMonitoringTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The monitoring target refers to the entity that is subject to analysis. e.g. Vertex AI Model version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesreasoningenginespecsourcecodespecpythonspec_g_b013bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecsourcecodespecpythonspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.PythonSpec -->

# Class PythonSpec (1.134.0)

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Attributes |
|
|---|---|
Name |
Description |
`version` |
`str`
Optional. The version of Python to use. Support version includes 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, default value is 3.10. |
`entrypoint_module` |
`str`
Optional. The Python module to load as the entrypoint, specified as a fully qualified module name. For example: path.to.agent. If not specified, defaults to "agent". The project root will be added to Python sys.path, allowing imports to be specified relative to the root. |
`entrypoint_object` |
`str`
Optional. The name of the callable object within the `entrypoint_module` to use as the application If not
specified, defaults to "root_agent".
|
`requirements_file` |
`str`
Optional. The path to the requirements file, relative to the source root. If not specified, defaults to "requirements.txt". |

## Methods

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawPredictRequest -->

# Class RawPredictRequest (1.134.0)

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`http_body` |
`google.api.httpbody_pb2.HttpBody`
The prediction input. Supports HTTP headers and arbitrary data payload. A DeployedModel may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the RawPredict method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model. You can specify the schema for each instance in the predict_schemata.instance_schema_uri field when you create a Model. This schema applies when you deploy the `Model` as a `DeployedModel`
to an Endpoint
and use the `RawPredict` method.
|

## Methods

### RawPredictRequest

`RawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.RawPredict.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicespipeline_servicepagerslisttrainingpipelinesasyn_289abe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespipeline_servicepagerslisttrainingpipelinesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager -->

# Class ListTrainingPipelinesAsyncPager (1.134.0)

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

## Methods

### ListTrainingPipelinesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatefeatureviewrequest_googlecloudaiplatfor_78a795.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeatureviewrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureViewRequest -->

# Class CreateFeatureViewRequest (1.134.0)

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`feature_view` |
Required. The FeatureView to create. |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a FeatureOnlineStore.
|
`run_sync_immediately` |
`bool`
Immutable. If set to true, one on demand sync will be run immediately, regardless whether the FeatureView.sync_config is configured or not. |

## Methods

### CreateFeatureViewRequest

`CreateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.CreateFeatureView.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeaturegrouprequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureGroupRequest -->

# Class UpdateFeatureGroupRequest (1.134.0)

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group` |
Required. The FeatureGroup's `name` field is used to
identify the FeatureGroup to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `big_query`
- `big_query.entity_id_columns`
|

## Methods

### UpdateFeatureGroupRequest

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesjob_servicepagerslisthyperparametertuningjobsp_af2699.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerslisthyperparametertuningjobspa_40d6ec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslisthyperparametertuningjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsPager -->

# Class ListHyperparameterTuningJobsPager (1.134.0)

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

## Methods

### ListHyperparameterTuningJobsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistbatchpredictionjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager -->

# Class ListBatchPredictionJobsAsyncPager (1.134.0)

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

## Methods

### ListBatchPredictionJobsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigpredictiondriftdete_850cdc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigpredictiondriftdetec_f977be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigpredictiondriftdetectionconfigattributionscoredriftthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.AttributionScoreDriftThresholdsEntry -->

# Class AttributionScoreDriftThresholdsEntry (1.134.0)

```
AttributionScoreDriftThresholdsEntry(
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

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesaddcontextartifactsandexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextArtifactsAndExecutionsRequest -->

# Class AddContextArtifactsAndExecutionsRequest (1.134.0)

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`artifacts` |
`MutableSequence[str]`
The resource names of the Artifacts to attribute to the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`executions` |
`MutableSequence[str]`
The resource names of the Executions to associate with the Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### AddContextArtifactsAndExecutionsRequest

```
AddContextArtifactsAndExecutionsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.AddContextArtifactsAndExecutions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesartifact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Artifact -->

# Class Artifact (1.134.0)

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Artifact. |
`display_name` |
`str`
User provided display name of the Artifact. May be up to 128 Unicode characters. |
`uri` |
`str`
The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was last updated. |
`state` |
The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Artifact |

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

### State

`State(value)`


Describes the state of the Artifact.

## Methods

### Artifact

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstudyspec___googlecloudaiplatform_v1typesmodelmon_8adcfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstudyspec___googlecloudaiplatform_v1typesmodelmoni_b7d201.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictions_be0727.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictionsk_a2a568.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfigattributionscoreskewthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.AttributionScoreSkewThresholdsEntry -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdnspeeringconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DnsPeeringConfig -->

# Class DnsPeeringConfig (1.134.0)

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

## Attributes |
|
|---|---|
Name |
Description |
`domain` |
`str`
Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot. |
`target_project` |
`str`
Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Vertex AI Service Agent requires the dns.peer role on this project. |
`target_network` |
`str`
Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible. |

## Methods

### DnsPeeringConfig

`DnsPeeringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelversioncheckpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsPager -->

# Class ListModelVersionCheckpointsPager (1.134.0)

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
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


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsPager

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardtimese_e429cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardtimeser_a04b78.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardtimeseriespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesPager -->

# Class ListTensorboardTimeSeriesPager (1.134.0)

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__iter__`

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

### ListTensorboardTimeSeriesPager

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessummarizationhelpfulnessresult_googlecloudaiplatfo_aefbda.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessummarizationhelpfulnessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessResult -->

# Class SummarizationHelpfulnessResult (1.134.0)

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization helpfulness score. |
`confidence` |
`float`
Output only. Confidence for summarization helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationHelpfulnessResult

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctioncallingconfigmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionCallingConfig.Mode -->

# Class Mode (1.134.0)

`Mode(value)`


Function calling mode.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Unspecified function calling mode. This value should not be used. |
`AUTO` |
Default model behavior, model decides to predict either function calls or natural language response. |
`ANY` |
Model is constrained to always predicting function calls only. If `allowed_function_names][FunctionCallingConfig.allowed_function_names]` are set, the predicted function calls will be limited to any one of `allowed_function_names`, else the predicted function calls will be any one of the provided [FunctionDeclaration]. |
`NONE` |
Model will not predict any function calls. Model behavior is same as when not passing any function declarations. |
`VALIDATED` |
Model is constrained to predict either function calls or natural language response. If `allowed_function_names][FunctionCallingConfig.allowed_function_names]` are set, the predicted function calls will be limited to any one of `allowed_function_names`, else the predicted function calls will be any one of the provided [FunctionDeclaration]. |

## Methods

### Mode

`Mode(value)`


Function calling mode.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesexample_store_servicepagerslistexamplestor_3532d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesexample_store_servicepagerslistexamplestoresasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresAsyncPager -->

# Class ListExampleStoresAsyncPager (1.134.0)

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

## Methods

### ListExampleStoresAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsAsyncPager -->

# Class ListModelEvaluationsAsyncPager (1.134.0)

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsAsyncPager

```
ListModelEvaluationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagers____googlecloudaiplatform_19f029.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.job_service.pagers`

module.

## Classes

[ListBatchPredictionJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
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

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListBatchPredictionJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsPager)

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
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

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListCustomJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsAsyncPager)

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

[ListCustomJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsPager)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse) object, and
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

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsAsyncPager)

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse) object, and
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

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsPager)

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

[ListHyperparameterTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager)

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
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

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsPager)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
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

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager)

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

[ListModelDeploymentMonitoringJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager)

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse) object, and
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

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsAsyncPager)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
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

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasJobsPager)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasJobsResponse,
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
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse) object, and
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

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsAsyncPager)

```
ListNasTrialDetailsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse) object, and
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

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsPager)

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

[SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
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

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager)

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


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationsl_2886b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationsli_cbd638.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationslic_37992f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelevaluationslicespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationSlicesPager -->

# Class ListModelEvaluationSlicesPager (1.134.0)

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
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


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesPager

```
ListModelEvaluationSlicesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesspecialist_pool_servicepagerslistspecialistpoolsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager -->

# Class ListSpecialistPoolsAsyncPager (1.134.0)

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
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

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsAsyncPager

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesevaluatedannotation_googlecloudaiplatform_v1beta1s_7eee6f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevaluatedannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotation -->

# Class EvaluatedAnnotation (1.134.0)

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Output only. Type of the EvaluatedAnnotation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The model predicted annotations. For true positive, there is one and only one prediction, which matches the only one ground truth annotation in ground_truths. For false positive, there is one and only one prediction, which doesn't match any ground truth annotation of the corresponding data_item_view_id. For false negative, there are zero or more predictions which are similar to the only ground truth annotation in ground_truths but not enough for a match. The schema of the prediction is stored in ModelEvaluation.annotation_schema_uri |
`ground_truths` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The ground truth Annotations, i.e. the Annotations that exist in the test data the Model is evaluated on. For true positive, there is one and only one ground truth annotation, which matches the only prediction in predictions. For false positive, there are zero or more ground truth annotations that are similar to the only prediction in predictions, but not enough for a match. For false negative, there is one and only one ground truth annotation, which doesn't match any predictions created by the model. The schema of the ground truth is stored in ModelEvaluation.annotation_schema_uri |
`data_item_payload` |
`google.protobuf.struct_pb2.Value`
Output only. The data item payload that the Model predicted this EvaluatedAnnotation on. |
`evaluated_data_item_view_id` |
`str`
Output only. ID of the EvaluatedDataItemView under the same ancestor ModelEvaluation. The EvaluatedDataItemView consists of all ground truths and predictions on data_item_payload. |
`explanations` |
`MutableSequence[`
Explanations of predictions. Each element of the explanations indicates the explanation for one explanation Method. The attributions list in the EvaluatedAnnotationExplanation.explanation object corresponds to the predictions list. For example, the second element in the attributions list explains the second element in the predictions list. |
`error_analysis_annotations` |
`MutableSequence[`
Annotations of model error analysis results. |

## Classes

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Methods

### EvaluatedAnnotation

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturemonitorjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager -->

# Class ListFeatureMonitorJobsPager (1.134.0)

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

## Methods

### ListFeatureMonitorJobsPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesvertex_rag_data_servicepagers__googlecloudaipla_d9ae02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningengi_b8d89a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesreasoning_engine_servicepagerslistreasoningenginesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager -->

# Class ListReasoningEnginesAsyncPager (1.134.0)

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
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

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListReasoningEnginesAsyncPager

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfunctiondeclaration.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionDeclaration -->

# Class FunctionDeclaration (1.134.0)

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64. |
`description` |
`str`
Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function. |
`parameters` |
Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1 |
`parameters_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: :: { "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] } This field is mutually exclusive with `parameters` .
|
`response` |
Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function. |
`response_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response` .
|

## Methods

### FunctionDeclaration

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagersli_dd3a99.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslis_976a76.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslist_0cecd8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistf_658c32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfe_75b9f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfea_08b700.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfeatureviewsyncspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager -->

# Class ListFeatureViewSyncsPager (1.134.0)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
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

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsPager

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_cache_servicepagerslistcachedcontentsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager -->

# Class ListCachedContentsAsyncPager (1.134.0)

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsAsyncPager

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessummarizationhelpfulnessresult_googlecloudai_101844.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessummarizationhelpfulnessresult_googlecloudaip_a1a6cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationhelpfulnessresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationHelpfulnessResult -->

# Class SummarizationHelpfulnessResult (1.134.0)

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Helpfulness score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization helpfulness score. |
`confidence` |
`float`
Output only. Confidence for summarization helpfulness score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationHelpfulnessResult

```
SummarizationHelpfulnessResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringQualityResult -->

# Class QuestionAnsweringQualityResult (1.134.0)

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringQualityResult

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespersistent_resource_servicepagerslistpersistentresourcespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesPager -->

# Class ListPersistentResourcesPager (1.134.0)

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

## Methods

### ListPersistentResourcesPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimetempl_c3e629.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimetempla_964ec3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimetemplatespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager -->

# Class ListNotebookRuntimeTemplatesPager (1.134.0)

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse) object, and
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

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesPager

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctiondeclaration.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionDeclaration -->

# Class FunctionDeclaration (1.134.0)

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64. |
`description` |
`str`
Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function. |
`parameters` |
Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1 |
`parameters_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: :: { "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] } This field is mutually exclusive with `parameters` .
|
`response` |
Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function. |
`response_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response` .
|

## Methods

### FunctionDeclaration

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schemapredictinstance_v1typestextextractionpredictionin_8a51fe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictinstance_v1typestextextractionpredictionins_3d5a95.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typestextextractionpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextExtractionPredictionInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricaggregationmetric.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Metric.AggregationMetric -->

# Class AggregationMetric (1.134.0)

`AggregationMetric(value)`


The aggregation metrics supported by EvaluationService.EvaluateDataset.

## Enums |
|
|---|---|
Name |
Description |
`AGGREGATION_METRIC_UNSPECIFIED` |
Unspecified aggregation metric. |
`AVERAGE` |
Average aggregation metric. Not supported for Pairwise metric. |
`MODE` |
Mode aggregation metric. |
`STANDARD_DEVIATION` |
Standard deviation aggregation metric. Not supported for pairwise metric. |
`VARIANCE` |
Variance aggregation metric. Not supported for pairwise metric. |
`MINIMUM` |
Minimum aggregation metric. Not supported for pairwise metric. |
`MAXIMUM` |
Maximum aggregation metric. Not supported for pairwise metric. |
`MEDIAN` |
Median aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P90` |
90th percentile aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P95` |
95th percentile aggregation metric. Not supported for pairwise metric. |
`PERCENTILE_P99` |
99th percentile aggregation metric. Not supported for pairwise metric. |

## Methods

### AggregationMetric

`AggregationMetric(value)`


The aggregation metrics supported by EvaluationService.EvaluateDataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookruntimesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager -->

# Class ListNotebookRuntimesAsyncPager (1.134.0)

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesAsyncPager

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagers____googlecl_30252d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeserroranalysisannotation_googlecloudaiplatfo_67c707.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeserroranalysisannotation_googlecloudaiplatfor_2e46fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeserroranalysisannotation_googlecloudaiplatform_7c88cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeserroranalysisannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ErrorAnalysisAnnotation -->

# Class ErrorAnalysisAnnotation (1.134.0)

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.

## Attributes |
|
|---|---|
Name |
Description |
`attributed_items` |
`MutableSequence[`
Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type. |
`query_type` |
The query type used for finding the attributed items. |
`outlier_score` |
`float`
The outlier score of this annotated item. Usually defined as the min of all distances from attributed items. |
`outlier_threshold` |
`float`
The threshold used to determine if this annotation is an outlier or not. |

## Classes

### AttributedItem

`AttributedItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Attributed items for a given annotation, typically representing neighbors from the training sets constrained by the query type.

### QueryType

`QueryType(value)`


The query type used for finding the attributed items.

## Methods

### ErrorAnalysisAnnotation

`ErrorAnalysisAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model error analysis for each annotation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetpublishermodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPublisherModelRequest -->

# Class GetPublisherModelRequest (1.134.0)

`GetPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.GetPublisherModel

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}`
|
`language_code` |
`str`
Optional. The IETF BCP-47 language code representing the language in which the publisher model's text information should be written in. |
`view` |
Optional. PublisherModel view specifying which fields to read. |
`is_hugging_face_model` |
`bool`
Optional. Boolean indicates whether the requested model is a Hugging Face model. |
`hugging_face_token` |
`str`
Optional. Token used to access Hugging Face gated models. |
`include_equivalent_model_garden_model_deployment_configs` |
`bool`
Optional. Whether to cnclude the deployment configs from the equivalent Model Garden model if the requested model is a Hugging Face model. |

## Methods

### GetPublisherModelRequest

`GetPublisherModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.GetPublisherModel


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmonitorsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitorsAsyncPager -->

# Class ListModelMonitorsAsyncPager (1.134.0)

```
ListModelMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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


A pager for iterating through `list_model_monitors`

requests.

This class thinly wraps an initial
[ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_monitors`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelMonitors`

requests and continue to iterate
through the `model_monitors`

field on the
corresponding responses.

All the usual [ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitorsAsyncPager

```
ListModelMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_servicepagersquer_6d4413.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdeployment_resource_pool_servicepagersquerydeployedmodelspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager -->

# Class QueryDeployedModelsPager (1.134.0)

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__iter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsPager

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesenterprisewebsearch_googlecloudaiplatform_v1b_b3daba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesenterprisewebsearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EnterpriseWebSearch -->

# Class EnterpriseWebSearch (1.134.0)

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### EnterpriseWebSearch

`EnterpriseWebSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to search public web data, powered by Vertex AI Search and Sec4 compliance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryprecisioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryPrecisionInstance -->

# Class TrajectoryPrecisionInstance (1.134.0)

`TrajectoryPrecisionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryPrecision instance.

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

### TrajectoryPrecisionInstance

`TrajectoryPrecisionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for TrajectoryPrecision instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatu_e1ca81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatur_4e2715.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeature_8428c9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeatureg_82b7d3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturegroupsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager -->

# Class ListFeatureGroupsAsyncPager (1.134.0)

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

## Methods

### ListFeatureGroupsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdatasetdistribution_googlecloudaiplatform_v1t_91986b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdatasetdistribution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetDistribution -->

# Class DatasetDistribution (1.134.0)

`DatasetDistribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Distribution computed over a tuning dataset.

## Attributes |
|
|---|---|
Name |
Description |
`sum` |
`float`
Output only. Sum of a given population of values. |
`min_` |
`float`
Output only. The minimum of the population values. |
`max_` |
`float`
Output only. The maximum of the population values. |
`mean` |
`float`
Output only. The arithmetic mean of the values in the population. |
`median` |
`float`
Output only. The median of the values in the population. |
`p5` |
`float`
Output only. The 5th percentile of the values in the population. |
`p95` |
`float`
Output only. The 95th percentile of the values in the population. |
`buckets` |
`MutableSequence[`
Output only. Defines the histogram bucket. |

## Classes

### DistributionBucket

`DistributionBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Methods

### DatasetDistribution

`DatasetDistribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Distribution computed over a tuning dataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringbigquerytable.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringBigQueryTable -->

# Class ModelDeploymentMonitoringBigQueryTable (1.134.0)

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

## Attributes |
|
|---|---|
Name |
Description |
`log_source` |
The source of log. |
`log_type` |
The type of log. |
`bigquery_table_path` |
`str`
The created BigQuery table to store logs. Customer could do their own query & analysis. Format: `bq://`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version of the request/response logging BigQuery table. Default to v1 if unset. |

## Classes

### LogSource

`LogSource(value)`


Indicates where does the log come from.

### LogType

`LogType(value)`


Indicates what type of traffic does the log belong to.

## Methods

### ModelDeploymentMonitoringBigQueryTable

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardru_cfe45a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardrunsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardRunsAsyncPager -->

# Class ListTensorboardRunsAsyncPager (1.134.0)

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardRunsAsyncPager

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesserviceaccountspec__googlecloudaiplatform_v1b_80975e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesserviceaccountspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ServiceAccountSpec -->

# Class ServiceAccountSpec (1.134.0)

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.

## Attributes |
|
|---|---|
Name |
Description |
`enable_custom_service_account` |
`bool`
Required. If true, custom user-managed service account is enforced to run any workloads (for example, Vertex Jobs) on the resource. Otherwise, uses the `Vertex AI Custom Code Service Agent |
`service_account` |
`str`
Optional. Required when all below conditions are met - `enable_custom_service_account` is true;
- any runtime is specified via `ResourceRuntimeSpec` on
creation time, for example, Ray
The users must have `iam.serviceAccounts.actAs` permission
on this service account and then the specified runtime
containers will run as it.
Do not set this field if you want to submit jobs using
custom service account to this PersistentResource after
creation, but only specify the `service_account` inside
the job.
|

## Methods

### ServiceAccountSpec

`ServiceAccountSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the use of custom service account to run the workloads.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesappendeventresponse_googlecloudaiplatform_v1b_2a347f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesappendeventresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AppendEventResponse -->

# Class AppendEventResponse (1.134.0)

`AppendEventResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.AppendEvent.

## Methods

### AppendEventResponse

`AppendEventResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.AppendEvent.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodality.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Modality -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmigration_servicepagerssearchmigratablere_a4afe1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmigration_servicepagerssearchmigratableres_78c67f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmigration_servicepagerssearchmigratableresourcespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager -->

# Class SearchMigratableResourcesPager (1.134.0)

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
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

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchMigratableResourcesPager

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookexecutionjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsPager -->

# Class ListNotebookExecutionJobsPager (1.134.0)

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsPager

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescometinstance_googlecloudaiplatform_v1beta1typest_9de20c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescometinstance_googlecloudaiplatform_v1beta1typesto_de86d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescometinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CometInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolgooglesearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.GoogleSearch -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_endpoint_servicepagerslistindexendpointsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager -->

# Class ListIndexEndpointsAsyncPager (1.134.0)

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsAsyncPager

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesupdatefeaturegrouprequest_googlecloudaipla_c449d0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatefeaturegrouprequest_googlecloudaiplat_5e1576.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeaturegrouprequest_googlecloudaiplatf_e18e29.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeaturegrouprequest_googlecloudaiplatfo_528d02.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeaturegrouprequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest -->

# Class UpdateFeatureGroupRequest (1.134.0)

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group` |
Required. The FeatureGroup's `name` field is used to
identify the FeatureGroup to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `description`
- `big_query`
- `big_query.entity_id_columns`
|

## Methods

### UpdateFeatureGroupRequest

`UpdateFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureGroup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoremonitoringconfigimportfeaturesanalysis.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis -->

# Class ImportFeaturesAnalysis (1.134.0)

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Whether to enable / disable / inherite default hebavior for import features analysis. |
`anomaly_detection_baseline` |
The baseline used to do anomaly detection for the statistics generated by import features analysis. |

## Classes

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Methods

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmutatedeployedmodelrequest_googlecloudaiplatform_v_fc1922.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmutatedeployedmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchcreatefeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragmanageddbconfig_googlecloudaiplatform_v1be_820091.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragmanageddbconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig -->

# Class RagManagedDbConfig (1.134.0)

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

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
`enterprise` |
Sets the RagManagedDb to the Enterprise tier. This field is a member of `oneof` _ `tier` .
|
`scaled` |
Sets the RagManagedDb to the Scaled tier. This is the default tier if not explicitly chosen. This field is a member of `oneof` _ `tier` .
|
`basic` |
Sets the RagManagedDb to the Basic tier. This field is a member of `oneof` _ `tier` .
|
`unprovisioned` |
Sets the RagManagedDb to the Unprovisioned tier. This field is a member of `oneof` _ `tier` .
|

## Classes

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

### Enterprise

`Enterprise(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Enterprise tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### RagManagedDbConfig

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagerslistspecialistpoolsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager -->

# Class ListSpecialistPoolsAsyncPager (1.134.0)

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

## Methods

### ListSpecialistPoolsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformhyperparametertuningjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob -->

# Class HyperparameterTuningJob (1.134.0)

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Vertex AI Hyperparameter Tuning Job.

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
HyperparameterTuningJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the HyperparameterTuningJob is not peered with any network.

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

### HyperparameterTuningJob

```
HyperparameterTuningJob(
display_name: str,
custom_job: google.cloud.aiplatform.jobs.CustomJob,
metric_spec: typing.Dict[str, str],
parameter_spec: typing.Dict[
str, google.cloud.aiplatform.hyperparameter_tuning._ParameterSpec
],
max_trial_count: int,
parallel_trial_count: int,
max_failed_trial_count: int = 0,
search_algorithm: typing.Optional[str] = None,
measurement_selection: typing.Optional[str] = "best",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
)
```


Configures a HyperparameterTuning Job.

Example usage:

```
from google.cloud.aiplatform import hyperparameter_tuning as hpt
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
custom_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
hp_job = aiplatform.HyperparameterTuningJob(
display_name='hp-test',
custom_job=job,
metric_spec={
'loss': 'minimize',
},
parameter_spec={
'lr': hpt.DoubleParameterSpec(min=0.001, max=0.1, scale='log'),
'units': hpt.IntegerParameterSpec(min=4, max=128, scale='linear'),
'activation': hpt.CategoricalParameterSpec(values=['relu', 'selu']),
'batch_size': hpt.DiscreteParameterSpec(values=[128, 256], scale='linear')
},
max_trial_count=128,
parallel_trial_count=8,
labels={'my_key': 'my_value'},
)
hp_job.run()
print(hp_job.trials)
```


For more information on using hyperparameter tuning please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning](https://cloud.google.com/ai-platform-unified/docs/training/using-hyperparameter-tuning)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`custom_job` |
`aiplatform.CustomJob`
Required. Configured CustomJob. The worker pool spec from this custom job applies to the CustomJobs created in all the trials. A persistent_resource_id can be specified on the custom job to be used when running this Hyperparameter Tuning job. |
`parameter_spec` |
`Dict[str, hyperparameter_tuning._ParameterSpec]`
Required. Dictionary representing parameters to optimize. The dictionary key is the metric_id, which is passed into your training job as a command line key word argument, and the dictionary value is the parameter specification of the metric. from google.cloud.aiplatform import hyperparameter_tuning as hpt parameter_spec={ 'decay': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear'), 'learning_rate': hpt.DoubleParameterSpec(min=1e-7, max=1, scale='linear') 'batch_size': hpt.DiscreteParamterSpec(values=[4, 8, 16, 32, 64, 128], scale='linear') } Supported parameter specifications can be found until aiplatform.hyperparameter_tuning. These parameter specification are currently supported: DoubleParameterSpec, IntegerParameterSpec, CategoricalParameterSpace, DiscreteParameterSpec |
`max_trial_count` |
`int`
Required. The desired total number of Trials. |
`parallel_trial_count` |
`int`
Required. The desired number of Trials to run in parallel. |
`max_failed_trial_count` |
`int`
Optional. The number of failed Trials that need to be seen before failing the HyperparameterTuningJob. If set to 0, Vertex AI decides how many Trials must fail before the whole job fails. |
`search_algorithm` |
`str`
The search algorithm specified for the Study. Accepts one of the following: |
`measurement_selection` |
`str`
This indicates which measurement to use if/when the service automatically selects the final measurement from previously reported intermediate measurements. Accepts: 'best', 'last' Choose this based on two considerations: A) Do you expect your measurements to monotonically improve? If so, choose 'last'. On the other hand, if you're in a situation where your system can "over-train" and you expect the performance to get better for a while but then start declining, choose 'best'. B) Are your measurements significantly noisy and/or irreproducible? If so, 'best' will tend to be over-optimistic, and it may be better to choose 'last'. If both or neither of (A) and (B) apply, it doesn't matter which selection type is chosen. |
`project` |
`str`
Optional. Project to run the HyperparameterTuningjob in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the HyperparameterTuning in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call HyperparameterTuning service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize HyperparameterTuningJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key options for a HyperparameterTuningJob. If this is set, then all resources created by the HyperparameterTuningJob will be encrypted with the provided encryption key. |

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
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
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
Optional. The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
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
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |

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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatf_2e7156.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatfo_7c3535.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatfor_ae8bf8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatform_6f9580.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatform__d34ee2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstreamingrawpredictrequest_googlecloudaiplatform_v_9e5571.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamingrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingRawPredictRequest -->

# Class StreamingRawPredictRequest (1.134.0)

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### StreamingRawPredictRequest

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardTimeSeriesRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigpredictiondrift_f4fa7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigpredictiondriftdetectionconfigattributionscoredriftthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.AttributionScoreDriftThresholdsEntry -->

# Class AttributionScoreDriftThresholdsEntry (1.134.0)

```
AttributionScoreDriftThresholdsEntry(
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

### AttributionScoreDriftThresholdsEntry

```
AttributionScoreDriftThresholdsEntry(
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatetensorboardexperimentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateTensorboardExperimentRequest -->

# Class UpdateTensorboardExperimentRequest (1.134.0)

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardExperiment resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_experiment` |
Required. The TensorboardExperiment's `name` field is used
to identify the TensorboardExperiment to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### UpdateTensorboardExperimentRequest

```
UpdateTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardExperiment.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeaturemonitorrequest_googlecloudaipla_475d17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeaturemonitorrequest_googlecloudaiplat_e4e6a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeaturemonitorrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest -->

# Class UpdateFeatureMonitorRequest (1.134.0)

`UpdateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`feature_monitor` |
Required. The FeatureMonitor's `name` field is used to
identify the FeatureMonitor to be updated. Format:
`projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
|

## Methods

### UpdateFeatureMonitorRequest

`UpdateFeatureMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.UpdateFeatureMonitor.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringQualityResult -->

# Class QuestionAnsweringQualityResult (1.134.0)

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringQualityResult

```
QuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfeatureviewsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager -->

# Class ListFeatureViewsAsyncPager (1.134.0)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
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

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewsAsyncPager

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistnotebookruntimesrequest_googlecloudaiplatform_f3c397.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistnotebookruntimesrequest_googlecloudaiplatform__63ec70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnotebookruntimesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesRequest -->

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
[google.cloud.aiplatform.v1.NotebookRuntime.name].
- `displayName` supports = and != and regex.
- `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1.NotebookRuntimeTemplate.name].
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardtimeseriespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesPager -->

# Class ListTensorboardTimeSeriesPager (1.134.0)

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesPager

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_garden_servicepagerslistpublishermod_990bb6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_garden_servicepagerslistpublishermodelsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsAsyncPager -->

# Class ListPublisherModelsAsyncPager (1.134.0)

```
ListPublisherModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPublisherModelsAsyncPager

```
ListPublisherModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfilechunkingconfig_googlecloudaiplatform_v_c303e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfilechunkingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileChunkingConfig -->

# Class RagFileChunkingConfig (1.134.0)

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`fixed_length_chunking` |
Specifies the fixed length chunking config. This field is a member of `oneof` _ `chunking_config` .
|
`chunk_size` |
`int`
The size of the chunks. |
`chunk_overlap` |
`int`
The overlap between chunks. |

## Classes

### FixedLengthChunking

`FixedLengthChunking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the fixed length chunking config.

## Methods

### RagFileChunkingConfig

`RagFileChunkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the size and overlap of chunks for RagFiles.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatefeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesevaluation_serviceevaluationserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient -->

# Class EvaluationServiceClient (1.134.0)

```
EvaluationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Vertex AI Online Evaluation Service.

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
`EvaluationServiceTransport` |
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

### EvaluationServiceClient

```
EvaluationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.evaluation_service.transports.base.EvaluationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the evaluation service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EvaluationServiceTransport,Callable[..., EvaluationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the EvaluationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### evaluate_dataset

```
evaluate_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateDatasetRequest,
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
) -> google.api_core.operation.Operation
```


Evaluates a dataset based on a set of given metrics.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_evaluate_dataset():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[EvaluationDataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluationDataset.html)()
dataset.gcs_source.uris = ['uris_value1', 'uris_value2']
output_config = aiplatform_v1beta1.[OutputConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputConfig.html)()
output_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[EvaluateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRequest.html)(
location="location_value",
dataset=dataset,
output_config=output_config,
)
# Make the request
operation = client.[evaluate_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceClient_evaluate_dataset)(request=request)
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
The request object. Request message for EvaluationService.EvaluateDataset. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
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

### evaluate_instances

```
evaluate_instances(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.evaluation_service.EvaluateInstancesResponse
```


Evaluates instances based on a given metric.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_evaluate_instances():
# Create a client
client = aiplatform_v1beta1.
```[EvaluationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[EvaluateInstancesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateInstancesRequest.html)(
location="location_value",
)
# Make the request
response = client.[evaluate_instances](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.evaluation_service.EvaluationServiceClient.html#google_cloud_aiplatform_v1beta1_services_evaluation_service_EvaluationServiceClient_evaluate_instances)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for EvaluationService.EvaluateInstances. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for EvaluationService.EvaluateInstances. |

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
`EvaluationServiceClient` |
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
`EvaluationServiceClient` |
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
`EvaluationServiceClient` |
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

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest__googlecloud_d30605.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest__googleclouda_5a70d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest__googlecloudai_b6fd85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest__googlecloudaip_38951d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest__googlecloudaipl_dd4775.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstreamingreadfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamingReadFeatureValuesRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltexte_42aff4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltextextractioninputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs -->

# Class AutoMlTextExtractionInputs (1.134.0)

`AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragcorpuscorpustypeconfigdocumentcorpus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.CorpusTypeConfig.DocumentCorpus -->

# Class DocumentCorpus (1.134.0)

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

## Methods

### DocumentCorpus

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespipeline_servicepagerslisttrainingpipelinesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager -->

# Class ListTrainingPipelinesAsyncPager (1.134.0)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
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
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse) object, and
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

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrainingPipelinesAsyncPager

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluatedannotation_googlecloudaiplatform_v1t_79c462.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluatedannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotation -->

# Class EvaluatedAnnotation (1.134.0)

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Output only. Type of the EvaluatedAnnotation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The model predicted annotations. For true positive, there is one and only one prediction, which matches the only one ground truth annotation in ground_truths. For false positive, there is one and only one prediction, which doesn't match any ground truth annotation of the corresponding `data_item_view_id][EvaluatedAnnotation.data_item_view_id]` .
For false negative, there are zero or more predictions which
are similar to the only ground truth annotation in
ground_truths
but not enough for a match.
The schema of the prediction is stored in
[ModelEvaluation.annotation_schema_uri][]
|
`ground_truths` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The ground truth Annotations, i.e. the Annotations that exist in the test data the Model is evaluated on. For true positive, there is one and only one ground truth annotation, which matches the only prediction in predictions. For false positive, there are zero or more ground truth annotations that are similar to the only prediction in predictions, but not enough for a match. For false negative, there is one and only one ground truth annotation, which doesn't match any predictions created by the model. The schema of the ground truth is stored in [ModelEvaluation.annotation_schema_uri][] |
`data_item_payload` |
`google.protobuf.struct_pb2.Value`
Output only. The data item payload that the Model predicted this EvaluatedAnnotation on. |
`evaluated_data_item_view_id` |
`str`
Output only. ID of the EvaluatedDataItemView under the same ancestor ModelEvaluation. The EvaluatedDataItemView consists of all ground truths and predictions on data_item_payload. |
`explanations` |
`MutableSequence[`
Explanations of predictions. Each element of the explanations indicates the explanation for one explanation Method. The attributions list in the EvaluatedAnnotationExplanation.explanation object corresponds to the predictions list. For example, the second element in the attributions list explains the second element in the predictions list. |
`error_analysis_annotations` |
`MutableSequence[`
Annotations of model error analysis results. |

## Classes

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Methods

### EvaluatedAnnotation

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformimagedataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset -->

# Class ImageDataset (1.134.0)

```
ImageDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


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

### ImageDataset

```
ImageDataset(
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
) -> google.cloud.aiplatform.datasets.image_dataset.ImageDataset
```


Creates a new image dataset.

Optionally imports data into the dataset when a source and
`import_schema_uri`

are passed in.

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
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each image in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Images and documents are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
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
`image_dataset (ImageDataset)` |
An instantiated representation of the managed `ImageDataset` resource. |

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeatures_472ee2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesa_6e7808.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesan_0addde.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesana_25cf5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesanalysis.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis -->

# Class ImportFeaturesAnalysis (1.134.0)

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Whether to enable / disable / inherite default hebavior for import features analysis. |
`anomaly_detection_baseline` |
The baseline used to do anomaly detection for the statistics generated by import features analysis. |

## Classes

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

### State

`State(value)`


The state defines whether to enable ImportFeature analysis.

## Methods

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringanomaly.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringAnomaly -->

# Class ModelMonitoringAnomaly (1.134.0)

`ModelMonitoringAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single model monitoring anomaly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tabular_anomaly` |
Tabular anomaly. This field is a member of `oneof` _ `anomaly` .
|
`model_monitoring_job` |
`str`
Model monitoring job resource name. |
`algorithm` |
`str`
Algorithm used to calculated the metrics, eg: jensen_shannon_divergence, l_infinity. |

## Classes

### TabularAnomaly

`TabularAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular anomaly details.

## Methods

### ModelMonitoringAnomaly

`ModelMonitoringAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single model monitoring anomaly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytable_google_f6e083.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringbigquerytable.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringBigQueryTable -->

# Class ModelDeploymentMonitoringBigQueryTable (1.134.0)

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

## Attributes |
|
|---|---|
Name |
Description |
`log_source` |
The source of log. |
`log_type` |
The type of log. |
`bigquery_table_path` |
`str`
The created BigQuery table to store logs. Customer could do their own query & analysis. Format: `bq://`
|
`request_response_logging_schema_version` |
`str`
Output only. The schema version of the request/response logging BigQuery table. Default to v1 if unset. |

## Classes

### LogSource

`LogSource(value)`


Indicates where does the log come from.

### LogType

`LogType(value)`


Indicates what type of traffic does the log belong to.

## Methods

### ModelDeploymentMonitoringBigQueryTable

```
ModelDeploymentMonitoringBigQueryTable(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamingrawpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingRawPredictRequest -->

# Class StreamingRawPredictRequest (1.134.0)

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`method_name` |
`str`
Fully qualified name of the API method being invoked to perform predictions. Format: `/namespace.Service/Method/` Example:
`/tensorflow.serving.PredictionService/Predict`
|
`input` |
`bytes`
The prediction input. |

## Methods

### StreamingRawPredictRequest

`StreamingRawPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingRawPredict.

The first message must contain endpoint and method_name fields and optionally input. The subsequent messages must contain input. method_name in the subsequent messages have no effect.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexplainrequest_googlecloudaiplatform_v1beta1_30d764.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplainrequest_googlecloudaiplatform_v1beta1s_2f508f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplainrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest -->

# Class ExplainRequest (1.134.0)

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. |
`explanation_spec_override` |
If specified, overrides the explanation_spec of the DeployedModel. Can be used for explaining prediction results with different configurations, such as: - Explaining top-5 predictions results as opposed to top-1; - Increasing path count or step count of the attribution methods to reduce approximate errors; - Using different baselines for explaining the prediction results. |
`concurrent_explanation_spec_override` |
`MutableMapping[str, `
Optional. This field is the same as the one above, but supports multiple explanations to occur in parallel. The key can be any string. Each override will be run against the model, then its explanations will be grouped together. Note - these explanations are run **In Addition** to the default Explanation in the deployed model. |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. |

## Classes

### ConcurrentExplanationSpecOverrideEntry

```
ConcurrentExplanationSpecOverrideEntry(
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

## Methods

### ExplainRequest

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagerslistfeatureviewsyncspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager -->

# Class ListFeatureViewSyncsPager (1.134.0)

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

## Methods

### ListFeatureViewSyncsPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslisthyperparametertuningj_dc499e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslisthyperparametertuningjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsPager -->

# Class ListHyperparameterTuningJobsPager (1.134.0)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
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

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListHyperparameterTuningJobsPager

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistbatchpredictionjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager -->

# Class ListBatchPredictionJobsAsyncPager (1.134.0)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
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

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListBatchPredictionJobsAsyncPager

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
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
