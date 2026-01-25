---
merged_at: 2026-01-25T12:06:29.152858
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleteworkerpoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteWorkerPoolRequest -->

# Class DeleteWorkerPoolRequest (0.14.0)

`DeleteWorkerPoolRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to delete a WorkerPool by its full name.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The full name of the WorkerPool. Format: `projects/{project}/locations/{location}/workerPools/{worker_pool}` ,
where `{project}` can be project id or number.
|
`validate_only` |
`bool`
Optional. Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. May be used to detect modification conflict during updates. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesconditionexecutionreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.ExecutionReason -->

# Class ExecutionReason (0.14.0)

`ExecutionReason(value)`


Reasons specific to Execution resource.

## Enums |
|
|---|---|
Name |
Description |
`EXECUTION_REASON_UNDEFINED` |
Default value. |
`JOB_STATUS_SERVICE_POLLING_ERROR` |
Internal system error getting execution status. System will retry. |
`NON_ZERO_EXIT_CODE` |
A task reached its retry limit and the last attempt failed due to the user container exiting with a non-zero exit code. |
`CANCELLED` |
The execution was cancelled by users. |
`CANCELLING` |
The execution is in the process of being cancelled. |
`DELETED` |
The execution was deleted. |
`DELAYED_START_PENDING` |
A delayed execution is waiting for a start time. |
