---
merged_at: 2026-01-26T20:50:51.814804
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesPager -->

# Class ListServicesPager (0.14.0)

```
ListServicesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.service.ListServicesResponse
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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


A pager for iterating through `list_services`

requests.

This class thinly wraps an initial
[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse) object, and
provides an `__iter__`

method to iterate through its
`services`

field.

If there are more pages, the `__iter__`

method will make additional
`ListServices`

requests and continue to iterate
through the `services`

field on the
corresponding responses.

All the usual [ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListServicesPager

```
ListServicesPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.service.ListServicesResponse
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VersionToPath -->

# Class VersionToPath (0.14.0)

`VersionToPath(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VersionToPath maps a specific version of a secret to a relative file to mount to, relative to VolumeMount's mount_path.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Required. The relative path of the secret in the container. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest value, or an integer or a secret alias for a specific version. |
`mode` |
`int`
Integer octal mode bits to use on this file, must be a value between 01 and 0777 (octal). If 0 or not set, the Volume's default mode will be used. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs -->

# Package jobs (0.14.0)

API documentation for run_v2.services.jobs.pagers module.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks -->

# Package tasks (0.14.0)

API documentation for run_v2.services.tasks.pagers module.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksAsyncPager -->

# Class ListTasksAsyncPager (0.14.0)

```
ListTasksAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.task.ListTasksResponse]
],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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


A pager for iterating through `list_tasks`

requests.

This class thinly wraps an initial
[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse) object, and
provides an `__aiter__`

method to iterate through its
`tasks`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTasks`

requests and continue to iterate
through the `tasks`

field on the
corresponding responses.

All the usual [ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTasksAsyncPager

```
ListTasksAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.task.ListTasksResponse]
],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.revisions.pagers.ListRevisionsPager -->

# Class ListRevisionsPager (0.14.0)

```
ListRevisionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.revision.ListRevisionsResponse
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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


A pager for iterating through `list_revisions`

requests.

This class thinly wraps an initial
[ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse) object, and
provides an `__iter__`

method to iterate through its
`revisions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRevisions`

requests and continue to iterate
through the `revisions`

field on the
corresponding responses.

All the usual [ListRevisionsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRevisionsPager

```
ListRevisionsPager(
method: typing.Callable[
[...], google.cloud.run_v2.types.revision.ListRevisionsResponse
],
request: google.cloud.run_v2.types.revision.ListRevisionsRequest,
response: google.cloud.run_v2.types.revision.ListRevisionsResponse,
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

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesbuildconfig__googlecloudrun_v2typesbuildconfigenvironment_4190e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesbuildconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig -->

# Class BuildConfig (0.14.0)

`BuildConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the Build step of the function that builds a container from the given source.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The Cloud Build name of the latest successful deployment of the function. |
`source_location` |
`str`
The Cloud Storage bucket URI where the function source code is located. |
`function_target` |
`str`
Optional. The name of the function (as defined in source code) that will be executed. Defaults to the resource name suffix, if not specified. For backward compatibility, if function with given name is not found, then the system will try to use function named "function". |
`image_uri` |
`str`
Optional. Artifact Registry URI to store the built image. |
`base_image` |
`str`
Optional. The base image used to build the function. |
`enable_automatic_updates` |
`bool`
Optional. Sets whether the function will receive automatic base image updates. |
`worker_pool` |
`str`
Optional. Name of the Cloud Build Custom Worker Pool that should be used to build the Cloud Run function. The format of this field is `projects/{project}/locations/{region}/workerPools/{workerPool}`
where `{project}` and `{region}` are the project id and
region respectively where the worker pool is defined and
`{workerPool}` is the short name of the worker pool.
|
`environment_variables` |
`MutableMapping[str, str]`
Optional. User-provided build-time environment variables for the function |
`service_account` |
`str`
Optional. Service account to be used for building the container. The format of this field is `projects/{projectId}/serviceAccounts/{serviceAccountEmail}` .
|

## Classes

### EnvironmentVariablesEntry

`EnvironmentVariablesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesbuildconfigenvironmentvariablesentry_googlecloudrun_v2typ_588877.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesbuildconfigenvironmentvariablesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildConfig.EnvironmentVariablesEntry -->

# Class EnvironmentVariablesEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesexecutionreferencecompletionstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference.CompletionStatus -->

# Class CompletionStatus (0.14.0)

The default value. This value is used if the state is omitted.

EXECUTION_SUCCEEDED

Job execution has succeeded.

EXECUTION_FAILED

Job execution has failed.

EXECUTION_RUNNING

Job execution is running normally.

EXECUTION_PENDING

Waiting for backing resources to be provisioned.

EXECUTION_CANCELLED

Job execution has been cancelled by the user.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesgcsvolumesource_googlecloudrun_v2typessubmitbuildrequest_e005ff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesgcsvolumesource_googlecloudrun_v2typessubmitbuildrequestb_55228c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgcsvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GCSVolumeSource -->

# Class GCSVolumeSource (0.14.0)

Represents a volume backed by a Cloud Storage bucket using
Cloud Storage FUSE.

Attributes

Name

Description

bucket

str
Cloud Storage Bucket name.

read_only

bool
If true, the volume will be mounted as read
only for all mounts.

mount_options

MutableSequence[str]
A list of additional flags to pass to the
gcsfuse CLI. Options should be specified without
the leading "--".

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildrequestbuildpacksbuildenvironmentvariablesentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.BuildpacksBuild.EnvironmentVariablesEntry -->

# Class EnvironmentVariablesEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typescreateservicerequest_googlecloudrun_v2typesrunjobrequest.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescreateservicerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateServiceRequest -->

# Class CreateServiceRequest (0.14.0)

`CreateServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a Service.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this service should be created. Format: projects/{project}/locations/{location}, where {project} can be project id or number. Only lowercase characters, digits, and hyphens. |
`service` |
Required. The Service instance to create. |
`service_id` |
`str`
Required. The unique identifier for the Service. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the service becomes {parent}/services/{service_id}. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest -->

# Class RunJobRequest (0.14.0)

`RunJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to create a new Execution of a Job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the Job. Format: projects/{project}/locations/{location}/jobs/{job}, where {project} can be project id or number. |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |
`overrides` |
Overrides specification for a given execution of a job. If provided, overrides will be applied to update the execution or task spec. |

## Classes

### Overrides

`Overrides(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RunJob Overrides that contains Execution fields to be overridden.
