---
merged_at: 2026-01-25T12:06:29.152112
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typescancelexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.CancelExecutionRequest -->

# Class CancelExecutionRequest (0.14.0)

`CancelExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for deleting an Execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Execution to cancel. Format: `projects/{project}/locations/{location}/jobs/{job}/executions/{execution}` ,
where `{project}` can be project id or number.
|
`validate_only` |
`bool`
Indicates that the request should be validated without actually cancelling any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. This may be used to detect modification conflict during updates. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesinstancesplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplit -->

# Class InstanceSplit (0.14.0)

str
Revision to which to assign this portion of
instances, if split allocation is by revision.

percent

int
Specifies percent of the instance split to
this Revision. This defaults to zero if
unspecified.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
