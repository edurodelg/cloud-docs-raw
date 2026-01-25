---
merged_at: 2026-01-25T12:06:29.161440
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typestaskattemptresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.TaskAttemptResult -->

# Class TaskAttemptResult (0.14.0)

`TaskAttemptResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Result of a task attempt.

## Attributes |
|
|---|---|
Name |
Description |
`status` |
`google.rpc.status_pb2.Status`
Output only. The status of this attempt. If the status code is OK, then the attempt succeeded. |
`exit_code` |
`int`
Output only. The exit code of this attempt. This may be unset if the container was unable to exit cleanly with a code due to some other failure. See status field for possible failure details. At most one of exit_code or term_signal will be set. |
`term_signal` |
`int`
Output only. Termination signal of the container. This is set to non-zero if the container is terminated by the system. At most one of exit_code or term_signal will be set. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typessubmitbuildresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.SubmitBuildResponse -->

# Class SubmitBuildResponse (0.14.0)

google.longrunning.operations_pb2.Operation
Cloud Build operation to be polled via
CloudBuild API.

base_image_uri

str
URI of the base builder image in Artifact
Registry being used in the build. Used to opt
into automatic base image updates.

base_image_warning

str
Warning message for the base image.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
