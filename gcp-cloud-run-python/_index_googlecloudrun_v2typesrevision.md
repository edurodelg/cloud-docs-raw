---
merged_at: 2026-01-25T12:06:29.185587
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrevision.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Revision -->

# Class Revision (0.14.0)

`Revision(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Revision is an immutable snapshot of code and configuration. A Revision references a container image. Revisions are only created by updates to its parent Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The unique name of this Revision. |
`uid` |
`str`
Output only. Server assigned unique identifier for the Revision. The value is a UUID4 string and guaranteed to remain unchanged until the resource is deleted. |
`generation` |
`int`
Output only. A number that monotonically increases every time the user modifies the desired state. |
`labels` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. |
`annotations` |
`MutableMapping[str, str]`
Output only. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The creation time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The last-modified time. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the deletion time. It is only populated as a response to a Delete request. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. For a deleted resource, the time after which it will be permamently deleted. It is only populated as a response to a Delete request. |
`launch_stage` |
`google.api.launch_stage_pb2.LaunchStage`
The least stable launch stage needed to create this resource, as defined by `Google Cloud Platform Launch Stages |
`service` |
`str`
Output only. The name of the parent service. |
`scaling` |
Scaling settings for this revision. |
`vpc_access` |
VPC Access configuration for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`max_instance_request_concurrency` |
`int`
Sets the maximum number of requests that each serving instance can receive. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Max allowed time for an instance to respond to a request. |
`service_account` |
`str`
Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
A list of Volumes to make available to containers. |
`execution_environment` |
The execution environment being used to host this Revision. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`service_mesh` |
Enables service mesh connectivity. |
`encryption_key_revocation_action` |
The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`reconciling` |
`bool`
Output only. Indicates whether the resource's reconciliation is still in progress. See comments in `Service.reconciling` for additional information on
reconciliation process in Cloud Run.
|
`conditions` |
`MutableSequence[`
Output only. The Condition of this Revision, containing its readiness status, and detailed error information in case it did not reach a serving state. |
`observed_generation` |
`int`
Output only. The generation of this Revision currently serving traffic. See comments in `reconciling` for
additional information on reconciliation process in Cloud
Run.
|
`log_uri` |
`str`
Output only. The Google Console URI to obtain logs for the Revision. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`session_affinity` |
`bool`
Enable session affinity. |
`scaling_status` |
Output only. The current effective scaling settings for the revision. |
`node_selector` |
The node selector for the revision. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. Output only. True if GPU zonal redundancy is disabled on this revision. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|
`creator` |
`str`
Output only. Email address of the authenticated creator. |
`etag` |
`str`
Output only. A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |

## Classes

### AnnotationsEntry

`AnnotationsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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
