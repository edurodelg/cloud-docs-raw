---
merged_at: 2026-01-26T23:13:32.272211
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetTaskRequest -->

# Class GetTaskRequest (0.14.0)

Request message for obtaining a Task by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Task.
Format:
projects/{project}/locations/{location}/jobs/{job}/executions/{execution}/tasks/{task}

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetJobRequest -->

# Class GetJobRequest (0.14.0)

Request message for obtaining a Job by its full name.

Attribute

Name

Description

name

str
Required. The full name of the Job.
Format:
projects/{project}/locations/{location}/jobs/{job},
where {project} can be project id or number.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetRevisionRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListRevisionsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ResourceRequirements -->

# Class ResourceRequirements (0.14.0)

`ResourceRequirements(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ResourceRequirements describes the compute resource requirements.

## Attributes |
|
|---|---|
Name |
Description |
`limits` |
`MutableMapping[str, str]`
Only `memory` , `cpu` and `nvidia.com/gpu` keys in the
map are supported.
.. raw:: html
Notes: * The only supported values for CPU are '1', '2', '4', and '8'. Setting 4 CPU requires at least 2Gi of memory. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. * For supported 'memory' values and syntax, go to https://cloud.google.com/run/docs/configuring/memory-limits * The only supported 'nvidia.com/gpu' value is '1'. |
`cpu_idle` |
`bool`
Determines whether CPU is only allocated during requests (true by default). However, if ResourceRequirements is set, the caller must explicitly set this field to true to preserve the default behavior. |
`startup_cpu_boost` |
`bool`
Determines whether CPU should be boosted on startup of a new container instance above the requested CPU threshold, this can help reduce cold-start latency. |

## Classes

### LimitsEntry

`LimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetServiceRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CloudSqlInstance -->

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
