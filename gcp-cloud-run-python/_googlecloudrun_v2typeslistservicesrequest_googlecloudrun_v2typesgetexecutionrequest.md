---
merged_at: 2026-01-25T12:06:29.157929
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistservicesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListServicesRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgetexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GetExecutionRequest -->

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
