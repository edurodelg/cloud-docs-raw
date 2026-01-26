---
merged_at: 2026-01-26T20:50:51.808724
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListWorkerPoolsRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TCPSocketAction -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskAttemptResult -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.VolumeMount -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListTasksRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EncryptionKeyRevocationAction -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ContainerPort -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest.Overrides -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Job.LabelsEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Task.LabelsEntry -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SecretVolumeSource -->

# Class SecretVolumeSource (0.14.0)

`SecretVolumeSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The secret's value will be presented as the content of a file whose name is defined in the item path. If no items are defined, the name of the file is the secret.

## Attributes |
|
|---|---|
Name |
Description |
`secret` |
`str`
Required. The name of the secret in Cloud Secret Manager. Format: {secret} if the secret is in the same project. projects/{project}/secrets/{secret} if the secret is in a different project. |
`items` |
`MutableSequence[`
If unspecified, the volume will expose a file whose name is the secret, relative to VolumeMount.mount_path + VolumeMount.sub_path. If specified, the key will be used as the version to fetch from Cloud Secret Manager and the path will be the name of the file exposed in the volume. When items are defined, they must specify a path and a version. |
`default_mode` |
`int`
Integer representation of mode bits to use on created files by default. Must be a value between 0000 and 0777 (octal), defaulting to 0444. Directories within the path are not affected by this setting. Notes - Internally, a umask of 0222 will be applied to any non-zero value. - This is an integer representation of the mode bits. So, the octal integer value should look exactly as the chmod numeric notation with a leading zero. Some examples: for chmod 640 (u=rw,g=r), set to 0640 (octal) or 416 (base-10). For chmod 755 (u=rwx,g=rx,o=rx), set to 0755 (octal) or 493 (base-10). - This might be in conflict with other options that affect the file mode, like fsGroup, and the result can be other mode bits set. This might be in conflict with other options that affect the file mode, like fsGroup, and as a result, other mode bits could be set. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Service.LabelsEntry -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Revision.LabelsEntry -->

# Class LabelsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
