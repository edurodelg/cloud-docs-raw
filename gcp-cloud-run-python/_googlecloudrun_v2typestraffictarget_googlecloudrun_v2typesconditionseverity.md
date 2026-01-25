---
merged_at: 2026-01-25T12:06:29.150579
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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
