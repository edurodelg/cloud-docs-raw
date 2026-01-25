---
merged_at: 2026-01-25T12:06:29.173230
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrunjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RunJobRequest -->

# Class RunJobRequest (0.14.0)

`RunJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message to create a new Execution of a Job.

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
`overrides` |
Overrides specification for a given execution of a job. If provided, overrides will be applied to update the execution or task spec. |

## Classes

### Overrides

`Overrides(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RunJob Overrides that contains Execution fields to be overridden.


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
