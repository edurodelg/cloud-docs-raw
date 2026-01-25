---
merged_at: 2026-01-25T12:06:29.151338
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservicemultiregionsettings.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Service.MultiRegionSettings -->

# Class MultiRegionSettings (0.14.0)

MutableSequence[str]
Required. List of regions to deploy to,
including primary region.

multi_region_id

str
Optional. System-generated unique id for the
multi-region Service.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleteexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteExecutionRequest -->

# Class DeleteExecutionRequest (0.14.0)

`DeleteExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for deleting an Execution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Execution to delete. Format: `projects/{project}/locations/{location}/jobs/{job}/executions/{execution}` ,
where `{project}` can be project id or number.
|
`validate_only` |
`bool`
Indicates that the request should be validated without actually deleting any resources. |
`etag` |
`str`
A system-generated fingerprint for this version of the resource. This may be used to detect modification conflict during updates. |
