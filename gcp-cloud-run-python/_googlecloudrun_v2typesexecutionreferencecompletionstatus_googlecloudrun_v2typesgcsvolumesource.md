---
merged_at: 2026-01-25T12:06:29.172037
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesexecutionreferencecompletionstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference.CompletionStatus -->

# Class CompletionStatus (0.14.0)

The default value. This value is used if the state is omitted.

EXECUTION_SUCCEEDED

Job execution has succeeded.

EXECUTION_FAILED

Job execution has failed.

EXECUTION_RUNNING

Job execution is running normally.

EXECUTION_PENDING

Waiting for backing resources to be provisioned.

EXECUTION_CANCELLED

Job execution has been cancelled by the user.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesgcsvolumesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.GCSVolumeSource -->

# Class GCSVolumeSource (0.14.0)

Represents a volume backed by a Cloud Storage bucket using
Cloud Storage FUSE.

Attributes

Name

Description

bucket

str
Cloud Storage Bucket name.

read_only

bool
If true, the volume will be mounted as read
only for all mounts.

mount_options

MutableSequence[str]
A list of additional flags to pass to the
gcsfuse CLI. Options should be specified without
the leading "--".

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
