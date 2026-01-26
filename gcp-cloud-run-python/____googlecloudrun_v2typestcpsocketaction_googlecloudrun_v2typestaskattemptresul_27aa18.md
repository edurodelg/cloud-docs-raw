---
merged_at: 2026-01-26T20:50:51.813910
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typestcpsocketaction_googlecloudrun_v2typestaskattemptresult__961af9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typestcpsocketaction_googlecloudrun_v2typestaskattemptresult.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestcpsocketaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TCPSocketAction -->

# Class TCPSocketAction (0.14.0)

TCPSocketAction describes an action based on opening a socket

Attribute

Name

Description

port

int
Optional. Port number to access on the container. Must be in
the range 1 to 65535. If not specified, defaults to the
exposed port of the container, which is the value of
container.ports[0].containerPort.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestaskattemptresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskAttemptResult -->

# Class TaskAttemptResult (0.14.0)

`TaskAttemptResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Result of a task attempt.

## Attributes |
|
|---|---|
Name |
Description |
`status` |
`google.rpc.status_pb2.Status`
Output only. The status of this attempt. If the status code is OK, then the attempt succeeded. |
`exit_code` |
`int`
Output only. The exit code of this attempt. This may be unset if the container was unable to exit cleanly with a code due to some other failure. See status field for possible failure details. At most one of exit_code or term_signal will be set. |
`term_signal` |
`int`
Output only. Termination signal of the container. This is set to non-zero if the container is terminated by the system. At most one of exit_code or term_signal will be set. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typessubmitbuildresponse_googlecloudrun_v2typesvolumemount.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildResponse -->

# Class SubmitBuildResponse (0.14.0)

google.longrunning.operations_pb2.Operation
Cloud Build operation to be polled via
CloudBuild API.

base_image_uri

str
URI of the base builder image in Artifact
Registry being used in the build. Used to opt
into automatic base image updates.

base_image_warning

str
Warning message for the base image.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesvolumemount.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VolumeMount -->

# Class VolumeMount (0.14.0)

`VolumeMount(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


VolumeMount describes a mounting of a Volume within a container.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. This must match the Name of a Volume. |
`mount_path` |
`str`
Required. Path within the container at which the volume should be mounted. Must not contain ':'. For Cloud SQL volumes, it can be left empty, or must otherwise be `/cloudsql` . All instances defined in the Volume will be
available as `/cloudsql/[instance]` . For more information
on Cloud SQL volumes, visit
https://cloud.google.com/sql/docs/mysql/connect-run
|
`sub_path` |
`str`
Optional. Path within the volume from which the container's volume should be mounted. Defaults to "" (volume's root). |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typeslisttasksrequest_googlecloudrun_v2typesencryptionkeyrevo_aa239e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typeslisttasksrequest_googlecloudrun_v2typesencryptionkeyrevoc_023d14.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslisttasksrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksRequest -->

# Class ListTasksRequest (0.14.0)

`ListTasksRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Tasks.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Execution from which the Tasks should be listed. To list all Tasks across Executions of a Job, use "-" instead of Execution name. To list all Tasks across Jobs, use "-" instead of Job name. Format: projects/{project}/locations/{location}/jobs/{job}/executions/{execution} |
`page_size` |
`int`
Maximum number of Tasks to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListTasks. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesencryptionkeyrevocationaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EncryptionKeyRevocationAction -->

# Class EncryptionKeyRevocationAction (0.14.0)

Specifies behavior if an encryption key used by a resource is
revoked.

Enums

Name

Description

ENCRYPTION_KEY_REVOCATION_ACTION_UNSPECIFIED

Unspecified

PREVENT_NEW

Prevents the creation of new instances.

SHUTDOWN

Shuts down existing instances, and prevents creation of new ones.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesprobe.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Probe -->

# Class Probe (0.14.0)

`Probe(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Probe describes a health check to be performed against a container to determine whether it is alive or ready to receive traffic.

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
`initial_delay_seconds` |
`int`
Optional. Number of seconds after the container has started before the probe is initiated. Defaults to 0 seconds. Minimum value is 0. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. |
`timeout_seconds` |
`int`
Optional. Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Maximum value is 3600. Must be smaller than period_seconds. |
`period_seconds` |
`int`
Optional. How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Maximum value for liveness probe is 3600. Maximum value for startup probe is 240. Must be greater or equal than timeout_seconds. |
`failure_threshold` |
`int`
Optional. Minimum consecutive failures for the probe to be considered failed after having succeeded. Defaults to 3. Minimum value is 1. |
`http_get` |
Optional. HTTPGet specifies the http request to perform. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`tcp_socket` |
Optional. TCPSocket specifies an action involving a TCP port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|
`grpc` |
Optional. GRPC specifies an action involving a gRPC port. Exactly one of httpGet, tcpSocket, or grpc must be specified. This field is a member of `oneof` _ `probe_type` .
|

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typescontainerport_googlecloudrun_v2typesrunjobrequestoverrid_0e3368.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typescontainerport_googlecloudrun_v2typesrunjobrequestoverride_50e82d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescontainerport.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ContainerPort -->

# Class ContainerPort (0.14.0)

ContainerPort represents a network port in a single
container.

Attributes

Name

Description

name

str
If specified, used to specify which protocol
to use. Allowed values are "http1" and "h2c".

container_port

int
Port number the container listens on. This must be a valid
TCP port number, 0 < container_port="">< 65536.="">

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequestoverrides.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides -->

# Class Overrides (0.14.0)

`Overrides(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RunJob Overrides that contains Execution fields to be overridden.

## Attributes |
|
|---|---|
Name |
Description |
`container_overrides` |
`MutableSequence[`
Per container override specification. |
`task_count` |
`int`
Optional. The desired number of tasks the execution should run. Will replace existing task_count value. |
`timeout` |
`google.protobuf.duration_pb2.Duration`
Duration in seconds the task may be active before the system will actively try to mark it failed and kill associated containers. Will replace existing timeout_seconds value. |

## Classes

### ContainerOverride

`ContainerOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per-container override specification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesjoblabelsentry_googlecloudrun_v2typestasklabelsentry.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesjoblabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job.LabelsEntry -->

# Class LabelsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestasklabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Task.LabelsEntry -->

# Class LabelsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typestasktemplate__googlecloudrun_v2typesjobannotationsentry_g_0f14e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestasktemplate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskTemplate -->

# Class TaskTemplate (0.14.0)

`TaskTemplate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TaskTemplate describes the data a task should have when created from a template.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`containers` |
`MutableSequence[`
Holds the single container that defines the unit of execution for this task. |
`volumes` |
`MutableSequence[`
Optional. A list of Volumes to make available to containers. |
`max_retries` |
`int`
Number of retries allowed per Task, before marking this Task failed. Defaults to 3. This field is a member of `oneof` _ `retries` .
|
`timeout` |
`google.protobuf.duration_pb2.Duration`
Optional. Max allowed time duration the Task may be active before the system will actively try to mark it failed and kill associated containers. This applies per attempt of a task, meaning each retry can run for the full timeout. Defaults to 600 seconds. |
`service_account` |
`str`
Optional. Email address of the IAM service account associated with the Task of a Job. The service account represents the identity of the running task, and determines what permissions the task has. If not provided, the task will use the project's default service account. |
`execution_environment` |
Optional. The execution environment being used to host this Task. |
`encryption_key` |
`str`
A reference to a customer managed encryption key (CMEK) to use to encrypt this container image. For more information, go to https://cloud.google.com/run/docs/securing/using-cmek |
`vpc_access` |
Optional. VPC Access configuration to use for this Task. For more information, visit https://cloud.google.com/run/docs/configuring/connecting-vpc. |
`node_selector` |
Optional. The node selector for the task template. |
`gpu_zonal_redundancy_disabled` |
`bool`
Optional. True if GPU zonal redundancy is disabled on this task template. This field is a member of `oneof` _ `_gpu_zonal_redundancy_disabled` .
|


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesjobannotationsentry_googlecloudrun_v2typestaskannotations_418afd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesjobannotationsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job.AnnotationsEntry -->

# Class AnnotationsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestaskannotationsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Task.AnnotationsEntry -->

# Class AnnotationsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
