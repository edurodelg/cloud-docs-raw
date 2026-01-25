---
merged_at: 2026-01-25T15:25:49.595590
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesinstancesplitallocationtype_googlecloudrun_v2typestraffi_745fd1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesinstancesplitallocationtype_googlecloudrun_v2typestraffic_3408fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesinstancesplitallocationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.InstanceSplitAllocationType -->

# Class InstanceSplitAllocationType (0.14.0)

Allocates instances to the Service's latest ready Revision.

INSTANCE_SPLIT_ALLOCATION_TYPE_REVISION

Allocates instances to a Revision by name.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestraffictargetallocationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetAllocationType -->

# Class TrafficTargetAllocationType (0.14.0)

Allocates instances to the Service's latest ready Revision.

TRAFFIC_TARGET_ALLOCATION_TYPE_REVISION

Allocates instances to a Revision by name.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typestraffictargetstatus_googlecloudrun_v2typestraffictarget.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestraffictargetstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTargetStatus -->

# Class TrafficTargetStatus (0.14.0)

int
Specifies percent of the traffic to this
Revision.

tag

str
Indicates the string used in the URI to
exclusively reference this target.

uri

str
Displays the target URI.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestraffictarget.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TrafficTarget -->

# Class TrafficTarget (0.14.0)

`TrafficTarget(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Holds a single traffic routing entry for the Service. Allocations can be done to a specific Revision name, or pointing to the latest Ready Revision.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
The allocation type for this traffic target. |
`revision` |
`str`
Revision to which to send this portion of traffic, if traffic allocation is by revision. |
`percent` |
`int`
Specifies percent of the traffic to this Revision. This defaults to zero if unspecified. |
`tag` |
`str`
Indicates a string to be part of the URI to exclusively reference this target. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudrun_v2typesconditionseverity_googlecloudrun_v2typesservicemultiregi_4580a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesconditionseverity_googlecloudrun_v2typesservicemultiregio_a6618f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesconditionseverity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.Condition.Severity -->

# Class Severity (0.14.0)

Represents the severity of the condition failures.

Enums

Name

Description

SEVERITY_UNSPECIFIED

Unspecified severity

ERROR

Error severity.

WARNING

Warning severity.

INFO

Info severity.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


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

<!-- DOCUMENTO FUSIONADO: _googlecloudrun_v2typesdeleteexecutionrequest_googlecloudrun_v2typescancelexecut_c102a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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
