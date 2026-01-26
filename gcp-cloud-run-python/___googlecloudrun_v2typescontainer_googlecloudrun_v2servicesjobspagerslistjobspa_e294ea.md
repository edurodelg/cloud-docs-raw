---
merged_at: 2026-01-26T20:50:51.815701
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typescontainer_googlecloudrun_v2servicesjobspagerslistjobspage_7d3b60.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescontainer.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Container -->

# Class Container (0.14.0)

`Container(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single application container. This specifies both the container to run, the command to run in the container and the arguments to supply to it. Note that additional arguments can be supplied by the system to the container at runtime.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Name of the container specified as a DNS_LABEL (RFC 1123). |
`image` |
`str`
Required. Name of the container image in Dockerhub, Google Artifact Registry, or Google Container Registry. If the host is not provided, Dockerhub is assumed. |
`source_code` |
Optional. Location of the source. |
`command` |
`MutableSequence[str]`
Entrypoint array. Not executed within a shell. The docker image's ENTRYPOINT is used if this is not provided. |
`args` |
`MutableSequence[str]`
Arguments to the entrypoint. The docker image's CMD is used if this is not provided. |
`env` |
`MutableSequence[`
List of environment variables to set in the container. |
`resources` |
Compute Resource requirements by this container. |
`ports` |
`MutableSequence[`
List of ports to expose from the container. Only a single port can be specified. The specified ports must be listening on all interfaces (0.0.0.0) within the container to be accessible. If omitted, a port number will be chosen and passed to the container through the PORT environment variable for the container to listen on. |
`volume_mounts` |
`MutableSequence[`
Volume to mount into the container's filesystem. |
`working_dir` |
`str`
Container's working directory. If not specified, the container runtime's default will be used, which might be configured in the container image. |
`liveness_probe` |
Periodic probe of container liveness. Container will be restarted if the probe fails. |
`startup_probe` |
Startup probe of application within the container. All other probes are disabled if a startup probe is provided, until it succeeds. Container will not be added to service endpoints if the probe fails. |
`depends_on` |
`MutableSequence[str]`
Names of the containers that must start before this container. |
`base_image_uri` |
`str`
Base image for this container. Only supported for services. If set, it indicates that the service is enrolled into automatic base image update. |
`build_info` |
Output only. The build info of the container image. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicesjobspagerslistjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.jobs.pagers.ListJobsPager -->

# Class ListJobsPager (0.14.0)

```
ListJobsPager(
method: typing.Callable[[...], google.cloud.run_v2.types.job.ListJobsResponse],
request: google.cloud.run_v2.types.job.ListJobsRequest,
response: google.cloud.run_v2.types.job.ListJobsResponse,
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


A pager for iterating through `list_jobs`

requests.

This class thinly wraps an initial
[ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListJobs`

requests and continue to iterate
through the `jobs`

field on the
corresponding responses.

All the usual [ListJobsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListJobsPager

```
ListJobsPager(
method: typing.Callable[[...], google.cloud.run_v2.types.job.ListJobsResponse],
request: google.cloud.run_v2.types.job.ListJobsRequest,
response: google.cloud.run_v2.types.job.ListJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2servicestaskspagerslisttaskspager__googlecloudrun_v2typescreat_5ca272.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2servicestaskspagerslisttaskspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksPager -->

# Class ListTasksPager (0.14.0)

```
ListTasksPager(
method: typing.Callable[[...], google.cloud.run_v2.types.task.ListTasksResponse],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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


A pager for iterating through `list_tasks`

requests.

This class thinly wraps an initial
[ListTasksResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse) object, and
provides an `__iter__`

method to iterate through its
`tasks`

field.

If there are more pages, the `__iter__`

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

### ListTasksPager

```
ListTasksPager(
method: typing.Callable[[...], google.cloud.run_v2.types.task.ListTasksResponse],
request: google.cloud.run_v2.types.task.ListTasksRequest,
response: google.cloud.run_v2.types.task.ListTasksResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typescreateworkerpoolrequest_googlecloudrun_v2typesvpcaccessne_d55ed9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescreateworkerpoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CreateWorkerPoolRequest -->

# Class CreateWorkerPoolRequest (0.14.0)

`CreateWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for creating a WorkerPool.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project in which this worker pool should be created. Format: `projects/{project}/locations/{location}` , where
`{project}` can be project id or number. Only lowercase
characters, digits, and hyphens.
|
`worker_pool` |
Required. The WorkerPool instance to create. |
`worker_pool_id` |
`str`
Required. The unique identifier for the WorkerPool. It must begin with letter, and cannot end with hyphen; must contain fewer than 50 characters. The name of the worker pool becomes `{parent}/workerPools/{worker_pool_id}` .
|
`validate_only` |
`bool`
Optional. Indicates that the request should be validated and default values populated, without persisting the request or creating any resources. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvpcaccessnetworkinterface.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.NetworkInterface -->

# Class NetworkInterface (0.14.0)

`NetworkInterface(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Direct VPC egress settings.

## Attributes |
|
|---|---|
Name |
Description |
`network` |
`str`
Optional. The VPC network that the Cloud Run resource will be able to send traffic to. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If network is not specified, it will be looked up from the subnetwork. |
`subnetwork` |
`str`
Optional. The VPC subnetwork that the Cloud Run resource will get IPs from. At least one of network or subnetwork must be specified. If both network and subnetwork are specified, the given VPC subnetwork must belong to the given VPC network. If subnetwork is not specified, the subnetwork with the same name with the network will be used. |
`tags` |
`MutableSequence[str]`
Optional. Network tags applied to this Cloud Run resource. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.worker_pools.pagers.ListWorkerPoolsAsyncPager -->

# Class ListWorkerPoolsAsyncPager (0.14.0)

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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


A pager for iterating through `list_worker_pools`

requests.

This class thinly wraps an initial
[ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`worker_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListWorkerPools`

requests and continue to iterate
through the `worker_pools`

field on the
corresponding responses.

All the usual [ListWorkerPoolsResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListWorkerPoolsAsyncPager

```
ListWorkerPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse],
],
request: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsRequest,
response: google.cloud.run_v2.types.worker_pool.ListWorkerPoolsResponse,
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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateWorkerPoolRequest -->

# Class UpdateWorkerPoolRequest (0.14.0)

`UpdateWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a worker pool.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. The list of fields to be updated. |
`worker_pool` |
Required. The WorkerPool to be updated. |
`validate_only` |
`bool`
Optional. Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the WorkerPool does not exist, it will create a new one. The caller must have 'run.workerpools.create' permissions if this is set to true and the WorkerPool does not exist. |
`force_new_revision` |
`bool`
Optional. If set to true, a new revision will be created from the template even if the system doesn't detect any changes from the previously deployed revision. This may be useful for cases where the underlying resources need to be recreated or reinitialized. For example if the image is specified by label, but the underlying image digest has changed) or if the container performs deployment initialization work that needs to be performed again. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildRequest.DockerBuild -->

# Class DockerBuild (0.14.0)

Build the source using Docker. This means the source has a
Dockerfile.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus -->

# Class RevisionScalingStatus (0.14.0)

int
The current number of min instances
provisioned for this revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.CommonReason -->

# Class CommonReason (0.14.0)

`CommonReason(value)`


Reasons common to all types of conditions.

## Enums |
|
|---|---|
Name |
Description |
`COMMON_REASON_UNDEFINED` |
Default value. |
`UNKNOWN` |
Reason unknown. Further details will be in message. |
`REVISION_FAILED` |
Revision creation process failed. |
`PROGRESS_DEADLINE_EXCEEDED` |
Timed out waiting for completion. |
`CONTAINER_MISSING` |
The container image path is incorrect. |
`CONTAINER_PERMISSION_DENIED` |
Insufficient permissions on the container image. |
`CONTAINER_IMAGE_UNAUTHORIZED` |
Container image is not authorized by policy. |
`CONTAINER_IMAGE_AUTHORIZATION_CHECK_FAILED` |
Container image policy authorization check failed. |
`ENCRYPTION_KEY_PERMISSION_DENIED` |
Insufficient permissions on encryption key. |
`ENCRYPTION_KEY_CHECK_FAILED` |
Permission check on encryption key failed. |
`SECRETS_ACCESS_CHECK_FAILED` |
At least one Access check on secrets failed. |
`WAITING_FOR_OPERATION` |
Waiting for operation to complete. |
`IMMEDIATE_RETRY` |
System will retry immediately. |
`POSTPONED_RETRY` |
System will retry later; current attempt failed. |
`INTERNAL` |
An internal error occurred. Further information may be in the message. |
`VPC_NETWORK_NOT_FOUND` |
User-provided VPC network was not found. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BinaryAuthorization -->

# Class BinaryAuthorization (0.14.0)

`BinaryAuthorization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for Binary Authorization feature.

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
`use_default` |
`bool`
Optional. If True, indicates to use the default project's binary authorization policy. If False, binary authorization will be disabled. This field is a member of `oneof` _ `binauthz_method` .
|
`policy` |
`str`
Optional. The path to a binary authorization policy. Format: `projects/{project}/platforms/cloudRun/{policy-name}`
This field is a member of `oneof` _ `binauthz_method` .
|
`breakglass_justification` |
`str`
Optional. If present, indicates to use Breakglass using this justification. If use_default is False, then it must be empty. For more information on breakglass, see https://cloud.google.com/binary-authorization/docs/using-breakglass |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScaling -->

# Class RevisionScaling (0.14.0)

`RevisionScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for revision-level scaling settings.

## Attributes |
|
|---|---|
Name |
Description |
`min_instance_count` |
`int`
Optional. Minimum number of serving instances that this resource should have. |
`max_instance_count` |
`int`
Optional. Maximum number of serving instances that this resource should have. When unspecified, the field is set to the server default value of 100. For more information see https://cloud.google.com/run/docs/configuring/max-instances |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListJobsResponse -->

# Class ListJobsResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListJobs request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksResponse -->

# Class ListTasksResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListTasks request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.IngressTraffic -->

# Class IngressTraffic (0.14.0)

Both internal and Google Cloud Load Balancer traffic is allowed.

INGRESS_TRAFFIC_NONE

No ingress traffic is allowed.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
