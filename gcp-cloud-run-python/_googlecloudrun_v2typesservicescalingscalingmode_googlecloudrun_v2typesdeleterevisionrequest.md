---
merged_at: 2026-01-25T12:06:29.158635
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesservicescalingscalingmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ServiceScaling.ScalingMode -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesdeleterevisionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.DeleteRevisionRequest -->

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
