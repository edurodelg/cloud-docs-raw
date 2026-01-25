---
merged_at: 2026-01-25T15:25:49.596593
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesgetrevisionrequest_googlecloudrun_v2typeslistrevisionsre_2cde14.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesgetrevisionrequest_googlecloudrun_v2typeslistrevisionsreq_4171d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgetrevisionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetRevisionRequest -->

# Class GetRevisionRequest (0.14.0)

Request message for obtaining a Revision by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Revision.
Format:
projects/{project}/locations/{location}/services/{service}/revisions/{revision}

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistrevisionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsRequest -->

# Class ListRevisionsRequest (0.14.0)

`ListRevisionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Revisions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Service from which the Revisions should be listed. To list all Revisions across Services, use "-" instead of Service name. Format: projects/{project}/locations/{location}/services/{service} |
`page_size` |
`int`
Maximum number of revisions to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListRevisions. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesgetservicerequest_googlecloudrun_v2typescloudsqlinstance.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgetservicerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetServiceRequest -->

# Class GetServiceRequest (0.14.0)

Request message for obtaining a Service by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Service.
Format:
projects/{project}/locations/{location}/services/{service},
where {project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescloudsqlinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CloudSqlInstance -->

# Class CloudSqlInstance (0.14.0)

`CloudSqlInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a set of Cloud SQL instances. Each one will be available
under /cloudsql/[instance]. Visit
[https://cloud.google.com/sql/docs/mysql/connect-run](https://cloud.google.com/sql/docs/mysql/connect-run) for more
information on how to connect Cloud SQL and Cloud Run.

## Attribute |
|
|---|---|
Name |
Description |
`instances` |
`MutableSequence[str]`
The Cloud SQL instance connection names, as can be found in https://console.cloud.google.com/sql/instances. Visit https://cloud.google.com/sql/docs/mysql/connect-run for more information on how to connect Cloud SQL and Cloud Run. Format: {project}:{location}:{instance} |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesworkerpoolrevisiontemplate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate -->

# Class WorkerPoolRevisionTemplate (0.14.0)

`WorkerPoolRevisionTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


WorkerPoolRevisionTemplate describes the data a worker pool revision should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`revision` |
`str`
Optional. The unique name for the revision. If this field is omitted, it will be automatically generated based on the WorkerPool name. |
`labels` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that can be used to organize and categorize objects. User-provided labels are shared with Google's billing system, so they can be used to filter, or break down billing charges by team, component, environment, state, etc. For more information, visit https://cloud.google.com/resource-manager/docs/creating-managing-labels or https://cloud.google.com/run/docs/configuring/labels. Cloud Run API v2 does not support labels with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected. All system labels in
v1 now have a corresponding field in v2
WorkerPoolRevisionTemplate.
|
`annotations` |
`MutableMapping[str, str]`
Optional. Unstructured key value map that may be set by external tools to store and arbitrary metadata. They are not queryable and should be preserved when modifying objects. Cloud Run API v2 does not support annotations with `run.googleapis.com` , `cloud.googleapis.com` ,
`serving.knative.dev` , or `autoscaling.knative.dev`
namespaces, and they will be rejected. All system
annotations in v1 now have a corresponding field in v2
WorkerPoolRevisionTemplate.
This field follows Kubernetes annotations' namespacing,
limits, and rules.
|
`vpc_access` |
Optional. VPC Access configuration to use for this Revision. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the revision of the service. The service account represents the identity of the running revision, and determines what permissions the revision has. If not provided, the revision will use the project's default service account. |
`containers` |
`MutableSequence[`
Holds list of the containers that defines the unit of execution for this Revision. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`service_mesh` |
Optional. Enables service mesh connectivity. |
`encryption_key_revocation_action` |
Optional. The action to take if the encryption key is revoked. |
`encryption_key_shutdown_duration` |
`google.protobuf.duration_pb2.Duration`
Optional. If encryption_key_revocation_action is SHUTDOWN, the duration before shutting down all instances. The minimum increment is 1 hour. |
`node_selector` |
Optional. The node selector for the revision template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this worker pool. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
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
