---
merged_at: 2026-01-25T12:06:29.137702
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrevisionscalingstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScalingStatus -->

# Class RevisionScalingStatus (0.14.0)

int
The current number of min instances
provisioned for this revision.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesrevisionscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.RevisionScaling -->

# Class RevisionScaling (0.14.0)

`RevisionScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Settings for revision-level scaling settings.

## Attributes |
|
|---|---|
Name |
Description |
`min_instance_count` |
`int`
Optional. Minimum number of serving instances that this resource should have. |
`max_instance_count` |
`int`
Optional. Maximum number of serving instances that this resource should have. When unspecified, the field is set to the server default value of 100. For more information see https://cloud.google.com/run/docs/configuring/max-instances |
