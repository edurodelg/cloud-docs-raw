---
merged_at: 2026-01-25T12:20:14.954318
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesexecutionreference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.ExecutionReference -->

# Class ExecutionReference (0.14.0)

`ExecutionReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to an Execution. Use /Executions.GetExecution with the given name to get full execution including the latest status.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Name of the execution. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Creation timestamp of the execution. |
`completion_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Creation timestamp of the execution. |
`delete_time` |
`google.protobuf.timestamp_pb2.Timestamp`
The deletion time of the execution. It is only populated as a response to a Delete request. |
`completion_status` |
Status for the execution completion. |

## Classes

### CompletionStatus

`CompletionStatus(value)`


Possible execution completion status.


---

<!-- DOCUMENTO FUSIONADO: googlecloudrun_v2typesworkerpoolrevisiontemplateannotationsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/run/latest/google.cloud.run_v2.types.WorkerPoolRevisionTemplate.AnnotationsEntry -->

# Class AnnotationsEntry (0.14.0)

Keys and values corresponding to the fields of the message.

mapping

Union[dict, .Message]

A dictionary or message to be used to determine the values for this message.

ignore_unknown_fields

Optional(bool)

If True, do not raise errors for unknown fields. Only applied if mapping is a mapping type or there are keyword parameters.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-12 UTC."],[],[]]
