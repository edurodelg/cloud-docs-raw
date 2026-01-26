---
merged_at: 2026-01-26T23:13:32.272699
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesResponse -->

# Class ListServicesResponse (0.14.0)

str
A token indicating there are more items than page_size. Use
it in the next ListServices request to continue.

unreachable

MutableSequence[str]
Output only. For global requests, returns the
list of regions that could not be reached within
the deadline.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.UpdateServiceRequest -->

# Class UpdateServiceRequest (0.14.0)

`UpdateServiceRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for updating a service.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. The list of fields to be updated. |
`service` |
Required. The Service to be updated. |
`validate_only` |
`bool`
Indicates that the request should be validated and default values populated, without persisting the request or updating any resources. |
`allow_missing` |
`bool`
Optional. If set to true, and if the Service does not exist, it will create a new one. The caller must have 'run.services.create' permissions if this is set to true and the Service does not exist. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetWorkerPoolRequest -->

# Class GetWorkerPoolRequest (0.14.0)

Request message for obtaining a WorkerPool by its full name.

Attribute

Name

Description

name

str
Required. The full name of the WorkerPool. Format:
projects/{project}/locations/{location}/workerPools/{worker_pool},
where {project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesRequest -->

# Class ListServicesRequest (0.14.0)

`ListServicesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Services.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location and project to list resources on. Location must be a valid Google Cloud region, and cannot be the "-" wildcard. Format: projects/{project}/locations/{location}, where {project} can be project id or number. |
`page_size` |
`int`
Maximum number of Services to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListServices. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetExecutionRequest -->

# Class GetExecutionRequest (0.14.0)

Request message for obtaining a Execution by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Execution. Format:
projects/{project}/locations/{location}/jobs/{job}/executions/{execution},
where {project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling.ScalingMode -->

# Class ScalingMode (0.14.0)

The scaling mode for the service. If not provided, it
defaults to AUTOMATIC.

Enums

Name

Description

SCALING_MODE_UNSPECIFIED

Unspecified.

AUTOMATIC

Scale based on traffic between min and max instances.

MANUAL

Scale to exactly min instances and ignore max instances.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteRevisionRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.EmptyDirVolumeSource.Medium -->

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
