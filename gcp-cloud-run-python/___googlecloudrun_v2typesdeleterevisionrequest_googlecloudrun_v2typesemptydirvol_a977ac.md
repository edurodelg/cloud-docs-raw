---
merged_at: 2026-01-25T15:25:49.597533
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesdeleterevisionrequest_googlecloudrun_v2typesemptydirvolu_86068b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesdeleterevisionrequest_googlecloudrun_v2typesemptydirvolum_e0c73f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleterevisionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteRevisionRequest -->

# Class DeleteRevisionRequest (0.14.0)

`DeleteRevisionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for deleting a retired Revision. Revision lifecycle is usually managed by making changes to the parent Service. Only retired revisions can be deleted with this API.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Revision to delete. Format: projects/{project}/locations/{location}/services/{service}/revisions/{revision} |
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. This may be used to detect modification conflict during updates. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesemptydirvolumesourcemedium.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource.Medium -->

# Class Medium (0.14.0)

The different types of medium supported for EmptyDir.

Enums

Name

Description

MEDIUM_UNSPECIFIED

When not specified, falls back to the default implementation which is currently in memory (this may change over time).

MEMORY

Explicitly set the EmptyDir to be in memory. Uses tmpfs.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeslistworkerpoolsrequest_googlecloudrun_v2typeslistexecutio_31c9f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistworkerpoolsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsRequest -->

# Class ListWorkerPoolsRequest (0.14.0)

`ListWorkerPoolsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of WorkerPools.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project to list resources on. Location must be a valid Google Cloud region, and cannot be the "-" wildcard. Format: `projects/{project}/locations/{location}` , where
`{project}` can be project id or number.
|
`page_size` |
`int`
Maximum number of WorkerPools to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListWorkerPools. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest -->

# Class ListExecutionsRequest (0.14.0)

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Executions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Execution from which the Executions should be listed. To list all Executions across Jobs, use "-" instead of Job name. Format: `projects/{project}/locations/{location}/jobs/{job}` ,
where `{project}` can be project id or number.
|
`page_size` |
`int`
Maximum number of Executions to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListExecutions. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrevisiontemplate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionTemplate -->

# Class RevisionTemplate (0.14.0)

`RevisionTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RevisionTemplate describes the data a revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`revision` |
`str`
Optional. The unique name for the revision. If this field is omitted, it will be automatically generated based on the Service name. |
`labels` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. .. raw:: html Cloud Run API v2 does not support labels with |
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. .. raw:: html Cloud Run API v2 does not support annotations with This field follows Kubernetes annotations' namespacing, limits, and rules. |
`scaling` |
Optional. Scaling settings for this Revision. |
`vpc_access` |
Optional. VPC Access configuration to use for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Optional. Max allowed time for an instance to respond to a request. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. If not provided, the revision will use the project's default service account. |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`execution_environment` |
Optional. The sandbox environment to host this Revision. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`max_instance_request_concurrency` |
`int`
Optional. Sets the maximum number of requests that each serving instance can receive. If not specified or 0, concurrency defaults to 80 when requested `CPU >= 1` and
defaults to 1 when requested `CPU <>` .
|
`service_mesh` |
Optional. Enables service mesh connectivity. |
`encryption_key_revocation_action` |
Optional. The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
Optional. If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`session_affinity` |
`bool`
Optional. Enable session affinity. |
`health_check_disabled` |
`bool`
Optional. Disables health checking containers during deployment. |
`node_selector` |
Optional. The node selector for the revision template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this revision. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|

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
