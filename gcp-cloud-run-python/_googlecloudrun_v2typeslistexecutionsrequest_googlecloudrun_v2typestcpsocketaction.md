---
merged_at: 2026-01-25T12:06:29.160489
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typeslistexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ListExecutionsRequest -->

# Class ListExecutionsRequest (0.14.0)

`ListExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for retrieving a list of Executions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The Execution from which the Executions should be listed. To list all Executions across Jobs, use "-" instead of Job name. Format: `projects/{project}/locations/{location}/jobs/{job}` ,
where `{project}` can be project id or number.
|
`page_size` |
`int`
Maximum number of Executions to return in this call. |
`page_token` |
`str`
A page token received from a previous call to ListExecutions. All other parameters must match. |
`show_deleted` |
`bool`
If true, returns deleted (but unexpired) resources along with active ones. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestcpsocketaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TCPSocketAction -->

# Class TCPSocketAction (0.14.0)

TCPSocketAction describes an action based on opening a socket

Attribute

Name

Description

port

int
Optional. Port number to access on the container. Must be in
the range 1 to 65535. If not specified, defaults to the
exposed port of the container, which is the value of
container.ports[0].containerPort.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
