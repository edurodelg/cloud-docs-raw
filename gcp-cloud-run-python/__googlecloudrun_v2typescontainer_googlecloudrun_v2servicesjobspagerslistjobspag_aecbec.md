---
merged_at: 2026-01-25T15:25:49.600236
merged_files: 2
---

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
