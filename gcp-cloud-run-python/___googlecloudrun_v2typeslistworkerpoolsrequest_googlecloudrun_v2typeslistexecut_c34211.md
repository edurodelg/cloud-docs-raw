---
merged_at: 2026-01-26T23:13:32.273165
merged_files: 2
---


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
