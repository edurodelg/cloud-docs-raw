---
merged_at: 2026-01-29T15:33:46.866217
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers -->

# Module pagers (0.15.0)

API documentation for `run_v2.services.tasks.pagers`

module.

## Classes

[ListTasksAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksAsyncPager)

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

[ListTasksPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.tasks.pagers.ListTasksPager)

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.IngressTraffic -->

# Class IngressTraffic (0.15.0)

Both internal and Google Cloud Load Balancer traffic is allowed.

INGRESS_TRAFFIC_NONE

No ingress traffic is allowed.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateJobRequest -->

# Class UpdateJobRequest (0.15.0)

`UpdateJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a Job.

## Attributes |
|
|---|---|
Name |
Description |
`job` |
Required. The Job to be updated. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the Job does not exist, it will create a new one. Caller must have both create and update permissions for this call if this is set to true. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretKeySelector -->

# Class SecretKeySelector (0.15.0)

`SecretKeySelector(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SecretEnvVarSource represents a source for the value of an EnvVar.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret_name} if the secret is in the same project. projects/{project}/secrets/{secret_name} if the secret is in a different project. |
`version` |
`str`
The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceMesh -->

# Class ServiceMesh (0.15.0)

str
The Mesh resource name. Format:
projects/{project}/locations/global/meshes/{mesh}, where
{project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsResponse -->

# Class ListRevisionsResponse (0.15.0)

str
A token indicating there are more items than page_size. Use
it in the next ListRevisions request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListInstancesResponse -->

# Class ListInstancesResponse (0.15.0)

str
A token indicating there are more items than page_size. Use
it in the next ListInstances request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (0.15.0)

str
A token indicating there are more items than page_size. Use
it in the next ListExecutions request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsResponse -->

# Class ListWorkerPoolsResponse (0.15.0)

str
A token indicating there are more items than page_size. Use
it in the next ListWorkerPools request to continue.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.RevisionReason -->

# Class RevisionReason (0.15.0)

`RevisionReason(value)`


Reasons specific to Revision resource.

## Enums |
|
|---|---|
Name |
Description |
`REVISION_REASON_UNDEFINED` |
Default value. |
`PENDING` |
Revision in Pending state. |
`RESERVE` |
Revision is in Reserve state. |
`RETIRED` |
Revision is Retired. |
`RETIRING` |
Revision is being retired. |
`RECREATING` |
Revision is being recreated. |
`HEALTH_CHECK_CONTAINER_ERROR` |
There was a health check error. |
`CUSTOMIZED_PATH_RESPONSE_PENDING` |
Health check failed due to user error from customized path of the container. System will retry. |
`MIN_INSTANCES_NOT_PROVISIONED` |
A revision with min_instance_count > 0 was created and is reserved, but it was not configured to serve traffic, so it's not live. This can also happen momentarily during traffic migration. |
`ACTIVE_REVISION_LIMIT_REACHED` |
The maximum allowed number of active revisions has been reached. |
`NO_DEPLOYMENT` |
There was no deployment defined. This value is no longer used, but Services created in older versions of the API might contain this value. |
`HEALTH_CHECK_SKIPPED` |
A revision's container has no port specified since the revision is of a manually scaled service with 0 instance count |
`MIN_INSTANCES_WARMING` |
A revision with min_instance_count > 0 was created and is waiting for enough instances to begin a traffic migration. |

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Volume -->

# Class Volume (0.15.0)

`Volume(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Volume represents a named volume in a container.

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
`name` |
`str`
Required. Volume's name. |
`secret` |
Secret represents a secret that should populate this volume. This field is a member of `oneof` _ `volume_type` .
|
`cloud_sql_instance` |
For Cloud SQL volumes, contains the specific instances that should be mounted. Visit https://cloud.google.com/sql/docs/mysql/connect-run for more information on how to connect Cloud SQL and Cloud Run. This field is a member of `oneof` _ `volume_type` .
|
`empty_dir` |
Ephemeral storage used as a shared volume. This field is a member of `oneof` _ `volume_type` .
|
`nfs` |
For NFS Voumes, contains the path to the nfs Volume This field is a member of `oneof` _ `volume_type` .
|
`gcs` |
Persistent storage backed by a Google Cloud Storage bucket. This field is a member of `oneof` _ `volume_type` .
|

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest -->

# Python Client for Cloud Run

[Cloud Run](https://cloud.google.com/run/docs): is a managed compute platform that enables you to run containers that are invocable via requests or events.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a virtual environment using [venv](https://docs.python.org/3/library/venv.html). [venv](https://docs.python.org/3/library/venv.html) is a tool that
creates isolated Python environments. These isolated environments can have separate
versions of Python packages, which allows you to isolate one project’s dependencies
from the dependencies of other projects.

With [venv](https://docs.python.org/3/library/venv.html), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

### Code samples and snippets

Code samples and snippets live in the [samples/](https://github.com/googleapis/google-cloud-python/tree/main/packages/google-cloud-run/samples) folder.

#### Supported Python Versions

Our client libraries are compatible with all current [active](https://devguide.python.org/devcycle/#in-development-main-branch) and [maintenance](https://devguide.python.org/devcycle/#maintenance-branches) versions of
Python.

Python >= 3.7, including 3.14

#### Unsupported Python Versions

Python <= 3.6

If you are using an [end-of-life](https://devguide.python.org/devcycle/#end-of-life-branches)
version of Python, we recommend that you update as soon as possible to an actively supported version.

#### Mac/Linux

```
python3 -m venv <your-env>
source <your-env>/bin/activate
pip install google-cloud-run
```


#### Windows

```
py -m venv <your-env>
.\<your-env>\Scripts\activate
pip install google-cloud-run
```


### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/run/latest/summary_overview)for Cloud Run to see other available methods on the client.Read the

[Cloud Run Product documentation](https://cloud.google.com/run/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

## Logging

This library uses the standard Python `logging`

functionality to log some RPC events that could be of interest for debugging and monitoring purposes.
Note the following:

Logs may contain sensitive information. Take care to

**restrict access to the logs**if they are saved, whether it be on local storage or on Google Cloud Logging.Google may refine the occurrence, level, and content of various log messages in this library without flagging such changes as breaking.

**Do not depend on immutability of the logging events**.By default, the logging events from this library are not handled. You must

**explicitly configure log handling**using one of the mechanisms below.

### Simple, environment-based configuration

To enable logging for this library without any changes in your code, set the `GOOGLE_SDK_PYTHON_LOGGING_SCOPE`

environment variable to a valid Google
logging scope. This configures handling of logging events (at level `logging.DEBUG`

or higher) from this library in a default manner, emitting the logged
messages in a structured format. It does not currently allow customizing the logging levels captured nor the handlers, formatters, etc. used for any logging
event.

A logging scope is a period-separated namespace that begins with `google`

, identifying the Python module or package to log.

Valid logging scopes:

`google`

,`google.cloud.asset.v1`

,`google.api`

,`google.auth`

, etc.Invalid logging scopes:

`foo`

,`123`

, etc.

**NOTE**: If the logging scope is invalid, the library does not set up any logging handlers.

#### Environment-Based Examples

- Enabling the default handler for all Google-based loggers

```
export GOOGLE_SDK_PYTHON_LOGGING_SCOPE=google
```


- Enabling the default handler for a specific Google module (for a client library called
`library_v1`

):

```
export GOOGLE_SDK_PYTHON_LOGGING_SCOPE=google.cloud.library_v1
```


### Advanced, code-based configuration

You can also configure a valid logging scope using Python’s standard logging mechanism.

#### Code-Based Examples

- Configuring a handler for all Google-based loggers

```
import logging
from google.cloud import library_v1
base_logger = logging.getLogger("google")
base_logger.addHandler(logging.StreamHandler())
base_logger.setLevel(logging.DEBUG)
```


- Configuring a handler for a specific Google module (for a client library called
`library_v1`

):

```
import logging
from google.cloud import library_v1
base_logger = logging.getLogger("google.cloud.library_v1")
base_logger.addHandler(logging.StreamHandler())
base_logger.setLevel(logging.DEBUG)
```


### Logging details

Regardless of which of the mechanisms above you use to configure logging for this library, by default logging events are not propagated up to the root logger from the google-level logger. If you need the events to be propagated to the root logger, you must explicitly set

`logging.getLogger("google").propagate = True`

in your code.You can mix the different logging configurations above for different Google modules. For example, you may want use a code-based logging configuration for one library, but decide you need to also set up environment-based logging configuration for another library.

- If you attempt to use both code-based and environment-based configuration for the same module, the environment-based configuration will be ineffectual if the code -based configuration gets applied first.

The Google-specific logging configurations (default handlers for environment-based configuration; not propagating logging events to the root logger) get executed the first time

*any*client library is instantiated in your application, and only if the affected loggers have not been previously configured. (This is the reason for 2.i. above.)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitStatus -->

# Class InstanceSplitStatus (0.15.0)

str
Revision to which this instance split is
assigned.

percent

int
Specifies percent of the instance split to
this Revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VpcAccess.VpcEgress -->

# Class VpcEgress (0.15.0)

All outbound traffic is routed through the VPC connector.

PRIVATE_RANGES_ONLY

Only private IP ranges are routed through the VPC connector.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteJobRequest -->

# Class DeleteJobRequest (0.15.0)

`DeleteJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a Job by its full name.

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

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.BuildInfo -->

# Class BuildInfo (0.15.0)

str
Output only. Entry point of the function when
the image is a Cloud Run function.

source_location

str
Output only. Source code location of the
image.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers -->

# Module pagers (0.15.0)

API documentation for `run_v2.services.services.pagers`

module.

## Classes

[ListServicesAsyncPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesAsyncPager)

```
ListServicesAsyncPager(
method: typing.Callable[
[...], typing.Awaitable[google.cloud.run_v2.types.service.ListServicesResponse]
],
request: google.cloud.run_v2.types.service.ListServicesRequest,
response: google.cloud.run_v2.types.service.ListServicesResponse,
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


A pager for iterating through `list_services`

requests.

This class thinly wraps an initial
[ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse) object, and
provides an `__aiter__`

method to iterate through its
`services`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListServices`

requests and continue to iterate
through the `services`

field on the
corresponding responses.

All the usual [ListServicesResponse](/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListServicesPager](/python/docs/reference/run/latest/google.cloud.run_v2.services.services.pagers.ListServicesPager)

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
